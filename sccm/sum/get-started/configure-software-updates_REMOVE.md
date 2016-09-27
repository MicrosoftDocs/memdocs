---
<<<<<<< HEAD
# required metadata

title: Configure software updates | System Center Configuration Manager
=======
title: "Configure software updates in System Center Configuration Manager"
>>>>>>> c44d17c87ba6af4ff1375d49ee170e2cd39b78ca
ms.custom: na
ms.date: 09/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-sum
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40380e25-f563-40f8-b5ad-01c9a9698754
caps.latest.revision: 16
author: Dougeby

---
# Configure software updates in System Center Configuration Manager
Before the compliance assessment data of the software update displays in the System Center Configuration Manager console and before you can deploy software updates to client computers, you must complete the following steps: install and configure a software update point, synchronize the software updates metadata, and verify the configuration for settings that are associated with software updates.  

 When you have a Configuration Manager hierarchy, install and configure the software update point at the central administration site first, and then install and configure the software update points on other sites. Some settings are only available when you configure the software update point on the top-level site, which is the central administration site or the stand-alone primary site. There are different configuration options that you must consider depending on where the software update point is installed. Use the steps in the following table to install and configure the software update point, synchronize software updates, and configure the settings that are associated with software updates.  

##  <a name="BKMK_TopOfPage"></a> Configure Software Updates  
 Use the following steps and  procedures in this topic to configure software updates in Configuration Manager.  

|Step|Details|  
|----------|-------------|  
|[Step 1: Install and configure a software update point](#BKMK_InstallSUP)|The software update point is required on the central administration site and on the primary sites to enable the software updates compliance assessment and to deploy software updates to clients. The software update point is optional on secondary sites.|  
|[Step 2: Synchronize Software Updates](#BKMK_SUMSync)|Choose your synchronization method depending on connectivity from the software update point to the update source:<br /><br /> <br /><br /> **Synchronize software updates from a connected software update point**<br /><br /> Software updates synchronization is the process of retrieving software updates metadata from the Microsoft Update site and the replication of the metadata to all sites that are enabled for software updates in the Configuration Manager hierarchy. The software update point on the central administration site or on a stand-alone primary site retrieves software updates metadata from Microsoft Update. The child primary sites and secondary sites retrieve the software updates metadata from the software update point that is identified as the upstream update source. You must have access to the upstream update source to successfully synchronize software updates. See [Synchronize software updates from a connected software update point](#BKMK_SyncConnected).<br /><br /> <br /><br /> **Synchronize software updates from a disconnected software update point**<br /><br /> Automatic synchronization of software updates is not possible when the software update point at the central administration site or stand-alone primary site is disconnected from the Internet. To retrieve the latest software updates for a disconnected software update point, you must use the WSUSUtil tool to export the software updates metadata and the license terms files from a software update source, and then you must import the metadata and files to the disconnected software update point.  See [Synchronize software updates from a disconnected software update point](#BKMK_SyncDisconnected).|  
|[Step 3: Configure classifications and products to synchronize](#BKMK_ConfigureClassesProducts)|Perform this configuration on the central administration site or stand-alone primary site.<br /><br /> After you synchronize software updates without any classifications or products selected, you must configure the software updates classifications and products in the Software Update Point Component properties. After you configure the properties, repeat step 2 to initiate the software updates synchronization to retrieve the software updates that meet the configured criteria for classification and products.|  
|[Step 4: Verify software updates client settings and group policy configurations](#BKMK_AssociatedSettings)|There are Configuration Manager client settings and group policy configurations that are associated with software updates, and that you must verify before you deploy software updates.|  

##  <a name="BKMK_InstallSUP"></a> Step 1: Install and configure a software update point  

> [!IMPORTANT]  
>  Before you install the software update point site system role, you must verify that the server meets the required dependencies and determines the software update point infrastructure on the site. For more information about how to plan for software updates and to determine your software update point infrastructure, see [Plan for software updates in System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md).  

 The software update point is required on the central administration site and on the primary sites in order to enable software updates compliance assessment and to deploy software updates to clients. The software update point is optional on secondary sites. The software update point site system role must be created on a server that has WSUS installed. The software update point interacts with the WSUS services to configure the software update settings and to request synchronization of software updates metadata. When you have a Configuration Manager hierarchy, install and configure the software update point on the central administration site first, then on child primary sites, and then optionally, on secondary sites. When you have a stand-alone primary site, not a central administration site, install and configure the software update point on the primary site first, and then optionally, on secondary sites. Some settings are only available when you configure the software update point on a top-level site. There are different options that you must consider depending on where you installed the software update point.  

> [!IMPORTANT]  
>  You can install more than one software update points on a site. The first software update point that you install is configured as the synchronization source, which synchronizes the updates from Microsoft Update or from the upstream synchronization source. The other software update points on the site are configured as replicas of the first software update point. Therefore, some settings are not available after you install and configure the initial software update point.  

 You can add the software update point site system role to an existing site system server or you can create a new one. On the **System Role Selection** page of the **Create Site System Server Wizard** or **Add Site System Roles Wizard** , depending on whether you add the site system role to a new or existing site server, select **Software update point**, and then configure the software update point settings in the wizard. The settings are different depending on the version of Configuration Manager that you use. For more information about how to install site system roles, see [Install site system roles for System Center Configuration Manager](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Use the following sections for information about the software update point settings on a site.  

### Proxy server settings  
 You can configure the proxy server settings on different pages of the **Create Site System Server Wizard** or **Add Site System Roles Wizard** depending on the version of Configuration Manager that you use.  

-   You must configure the proxy server, and then specify when to use the proxy server for software updates. Configure the following settings:  

    -   Configure the proxy server settings on the **Proxy** page of the wizard or on the **Proxy** tab in Site system Properties. The proxy server settings are site system specific, which means that all site system roles use the proxy server settings that you specify.  

    -   Specify whether to use the proxy server when Configuration Manager synchronizes the software updates and when it downloads content by using an automatic deployment rule. Configure the software update point proxy server settings on the **Proxy and Account Settings** page of the wizard or on the **Proxy and Account Settings** tab in Software update point Properties.  

        > [!NOTE]  
        >  The **Use a proxy when downloading content by using automatic deployment rules** setting is available but it is not used for a software update point on a secondary site. Only the software update point on the central administration site and primary site downloads content from the Microsoft Update page.  

> [!IMPORTANT]  
>  By default, the **Local System** account for the server on which an automatic deployment rule was created is used to connect to the Internet and download software updates when the automatic deployment rules run. When this account does not have access to the Internet, software updates fail to download and the following entry is logged to ruleengine.log: **Failed to download the update from internet. Error = 12007**. Configure the credentials to connect to the proxy server when the Local System account does not have Internet access.  

### WSUS settings  
 You must configure WSUS settings on different pages of the **Create Site System Server Wizard** or **Add Site System Roles Wizard** depending on the version of Configuration Manager that you use, and in some cases, only in the properties for the software update point, also known as Software Update Point Component Properties. Use the information in the following sections to configure the WSUS settings.  

#### WSUS port settings  
 You must configure the WSUS port settings on the Software Update Point page of the wizard or in the properties of the software update point.  

 To determine the website and port configurations in WSUS, see [How to determine the port settings used by WSUS in System Center Configuration Manager](../../sum/plan-design/determine-wsus-port-settings.md).  

#### Configure SSL communications to WSUS  
 You can configure SSL communication on the **General** page of the wizard or on the **General** tab in the properties of the software update point.  

 For more information about how to use SSL, see [Decide whether to configure WSUS to use SSL](../../sum/plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

#### WSUS Server Connection Account  
 You can configure an account to be used by the site server when it connects to WSUS that runs on the software update point. When you do not configure this account, the Configuration Manager uses the computer account for the site server to connect to WSUS. Configure the WSUS Server Connection Account on the **Proxy and Account Settings** page of the wizard, or on the **Proxy and Account Settings** tab in Software update point Properties.  You can configure the account in different places of the wizard depending on the version of Configuration Manager that you use.  

 For more information about Configuration Manager accounts, see [Accounts used in System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

### Synchronization Source  
 You can configure the upstream synchronization source for software updates synchronization on the **Synchronization Source** page of the wizard, or on the on the **Sync Settings** tab in Software Update Point Component Properties. Your options for the synchronization source vary depending on the site. For more information, see [Synchronization source](../../sum/plan-design/plan-for-software-updates.md#BKMK_SyncSource).  

 Use the following table for the available options when you configure the software update point at a site.  

|Site|Available synchronization source options|  
|----------|----------------------------------------------|  
|-   Central administration site<br />-   Stand-alone primary site|-   Synchronize from the Microsoft Update website<br />-   Synchronize from an upstream data source location<br />-   Do not synchronize from Microsoft Update or upstream data source|  
|-   Additional software update points at a site<br />-   Child primary site<br />-   Secondary site|-   Synchronize from an upstream data source location|  

 The following list provides more information about each option that you can use as the synchronization source:  

-   **Synchronize from Microsoft Update**: Use this setting to synchronize software updates metadata from Microsoft Update. The central administration site must have Internet access; otherwise, synchronization will fail. This setting is available only when you configure the software update point on the top-level site.  

    > [!NOTE]  
    >  When there is a firewall between the software update point and the Internet, the firewall might need to be configured to accept the HTTP and HTTPS ports that are used for the WSUS Web site. You can also choose to restrict access on the firewall to limited domains. For more information about how to plan for a firewall that supports software updates, see [Configure firewalls](../../sum/plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **Synchronize from an upstream data source location**: Use this setting to synchronize software updates metadata from the upstream synchronization source. The child primary sites and secondary sites are automatically configured to use the parent site URL for this setting. You have the option to synchronize software updates from an existing WSUS server. Specify a URL, such as https://WSUSServer:8531, where 8531 is the port that is used to connect to the WSUS server.  

-   **Do not synchronize from Microsoft Update or upstream data source**: Use this setting to manually synchronize software updates when the software update point at the top-level site is disconnected from the Internet. For more information, see the [Synchronize software updates from a disconnected software update point](#BKMK_SyncDisconnected) section in this topic.  

> [!NOTE]  
>  When there is a firewall between the software update point and the Internet, the firewall might need to be configured to accept the HTTP and HTTPS ports that are used for the WSUS Web site. You can also choose to restrict access on the firewall to limited domains. For more information about how to plan for a firewall that supports software updates, see the [Configure firewalls](../../sum/plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls) section in the [Plan for software updates in System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md) topic.  

 You can also configure whether to create WSUS reporting events on the **Synchronization Source** page of the wizard or on the on the **Sync Settings** tab in Software Update Point Component Properties. Configuration Manager does not use these events; therefore, you will normally choose the default setting **Do not create WSUS reporting events**.  

### Synchronization schedule  
 Configure the synchronization schedule on the **Synchronization Schedule** page of the wizard or in the Software Update Point Component Properties. This setting is configured only on the software update point at the top-level site.  

 If you enable the schedule, you can configure a recurring simple or custom synchronization schedule. When you configure a simple schedule, the start time is based on the local time for the computer that runs the Configuration Manager console at the time when you create the schedule. When you configure the start time for a custom schedule, it is based on the local time for the computer that runs the Configuration Manager console.  

> [!TIP]  
>  Schedule software updates synchronization to run by using a time-frame that is appropriate for your environment. One typical scenario is to set the software updates synchronization schedule to run shortly after the Microsoft regular security update release on the second Tuesday of each month, which is normally referred to as Patch Tuesday. Another typical scenario is to set the software updates synchronization schedule to run daily when you use software updates to deliver the Endpoint Protection definition and engine updates.  

> [!NOTE]  
>  When you choose not to enable software updates synchronization on a schedule, you can manually synchronize software updates from the **All Software Updates** or **Software Update Groups** node in the Software Library workspace. For more information, see [Step 2: Synchronize Software Updates](#BKMK_SUMSync).  

### Supersedence rules  
 Configure the supersedence settings on the **Supersedence Rules** page of the wizard or on the **Supersedence Rules** tab in Software Update Point Component Properties. You can configure the supersedence rules only on the top-level site.  

 On this page, you can specify that the superseded software updates are immediately expired, which prevents them from being included in new deployments and flags the existing deployments to indicate that the superseded software updates contain one or more expired software updates. Or, you can specify a period of time before the superseded software updates are expired, which allows you to continue to deploy them. For more information, see [Supersedence rules](../../sum/plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  The **Supersedence Rules** page of the wizard is available only when you configure the first software update point at the site. This page is not displayed when you install additional software update points.  

### Classifications  
 Configure the classifications settings on the **Classifications** page of the wizard, or the on the **Classifications** tab in Software Update Point Component Properties. For more information about software update classifications, see the [Update classifications](../../sum/plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications) section in the [Plan for software updates in System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md) topic.  

> [!NOTE]  
>  The **Classifications** page of the wizard is available only when you configure the first software update point at the site. This page is not displayed when you install additional software update points.  

> [!TIP]  
>  When you first install the software update point on the top-level site, clear all of the software updates classifications. After the initial software updates synchronization, configure the classifications from an updated list, and then re-initiate synchronization. This setting is configured only on the software update point at the top-level site.  

### Products  
 Configure the product settings on the **Products** page of the wizard, or the on the **Products** tab in Software Update Point Component Properties.  

> [!NOTE]  
>  The **Products** page of the wizard is available only when you configure the first software update point at the site. This page is not displayed when you install additional software update points.  

> [!TIP]  
>  When you first install the software update point on the top-level site, clear all of the products. After the initial software updates synchronization, configure the products from an updated list, and then re-initiate synchronization. This setting is configured only on the software update point at the top-level site.  

### Languages  
 Configure the language settings on the **Languages** page of the wizard, or the on the **Languages** tab in Software Update Point Component Properties. Specify the languages for which you want to synchronize software update files and summary details. The **Software Update File** setting is configured at each software update point in the Configuration Manager hierarchy. The **Summary Details** settings are configured only on the top-level software update point. For more information, see [Languages](../../sum/plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  The **Languages** page of the wizard is available only when you install the software update point at the central administration site. You can configure the Software Update File languages at child sites from the **Languages** tab in Software Update Point Component Properties.  

##  <a name="BKMK_SUMSync"></a> Step 2: Synchronize Software Updates  
 Software updates synchronization in Configuration Manager is the process of retrieving the software updates metadata that meets the criteria that you configure on the top-level site. The software update point on the top-level site retrieves the metadata from the Microsoft Update website or from an existing WSUS server on a schedule, or you can manually initiate synchronization from the Configuration Manager console. To successfully complete the synchronization, the software update point must have access to its upstream synchronization source. When the software update point is disconnected from the upstream synchronization source, you must use the WSUSUtil tool to export software updates metadata from a software updates source and import the metadata to the disconnected software update point. The following table lists the software update point types and the upstream synchronization source for which the software update point requires access.  

|Software update point|Upstream synchronization source|  
|---------------------------|-------------------------------------|  
|Central administration site|Microsoft Update (Internet)<sup>1</sup><br /><br /> Existing WSUS server|  
|Stand-alone primary site|Microsoft Update (Internet)<sup>1</sup><br /><br /> Existing WSUS server|  
|Child primary site|Central administration site|  
|Secondary site|Parent primary site|  

 <sup>1</sup>When the software update point is disconnected from the upstream update source, you can manually perform software updates synchronization. For more information, see the [Synchronize software updates from a disconnected software update point](#BKMK_SyncDisconnected) section in this topic.  

###  <a name="BKMK_SyncConnected"></a> Synchronize software updates from a connected software update point  
 Typically, the software update points in your Configuration Manager hierarchy will have access to the upstream update source. In this scenario, the software update point at the top-level site will connect to the Internet and synchronize software updates from the Microsoft Update site, and then the top-level site will send a synchronization request to other sites to initiate the synchronization process. When a site receives the synchronization request from the top-level site, the software update point for the site retrieves software updates metadata from its upstream synchronization source.  

> [!NOTE]  
>  The software update point on child primary sites and secondary sites must be connected to their upstream synchronization source to synchronize software updates. When a software update point is disconnected from its upstream synchronization source, you can use the export and import method to synchronize software updates. For more information, see the [Synchronize software updates from a disconnected software update point](#BKMK_SyncDisconnected) section in this topic.  

 When software updates synchronization is initiated on a configured schedule, the top-level software update point initiates synchronization with Microsoft Update at the scheduled date and time. The custom schedule allows you to synchronize software updates on a date and time when the demands of the WSUS server, site server, and network are low, for example when it synchronizes every week at 2:00 AM. During the scheduled synchronization, all changes to the software updates metadata since the last scheduled synchronization are inserted into the site database. This includes new software updates metadata or metadata that has been modified, removed, or is now expired. After the synchronization with the upstream synchronization source is complete, a synchronization request is sent to software update points on child primary or secondary sites. You can also manually initiate software updates synchronization on the top-level site in the Configuration Manager console from the **All Software Updates** node in the **Software Library** workspace.  

 Use the following procedures on the top-level site to schedule or to manually initiate software updates synchronization.  

##### To schedule software updates synchronization  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the Administration workspace, expand **Site Configuration**, and then click **Sites**.  

3.  In the results pane, click the central administration site or stand-alone primary site.  

4.  On the **Home** tab, in the **Settings** group, expand **Configure Site Components**, and then click **Software Update Point**.  

5.  In the Software Update Point Component Properties dialog box, select **Enable synchronization on a schedule**, and then specify the synchronization schedule.  

##### To manually initiate software updates synchronization  

1.  In the Configuration Manager console that is connected to the central administration site or stand-alone primary site, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates** and click **All Software Updates** or **Software Update Groups**.  

3.  On the **Home** tab, in the **Create** group, click **Synchronize Software Updates**. Click **Yes** in the dialog box to confirm that you want to initiate the synchronization process.  

 After you initiate the synchronization process on the software update point, you can monitor the synchronization process from the Configuration Manager console for all software update points in your hierarchy. Use the following procedure to monitor the software updates synchronization process.  

##### To monitor the software updates synchronization process  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, click **Software Update Point Synchronization Status**.  

     The software update points in your Configuration Manager hierarchy are displayed in the results pane. From this view, you can monitor the synchronization status for all software update points. When you want more detailed information about the synchronization process, you can review the wsyncmgr.log file that is located in <*ConfigMgrInstallationPath*>\Logs on each site server.  

###  <a name="BKMK_SyncDisconnected"></a> Synchronize software updates from a disconnected software update point  
 When the software update point at the top-level site is disconnected from the Internet, you must use the export and import functions of the WSUSUtil tool to synchronize software updates metadata. You can choose an existing WSUS that is not in your Configuration Manager hierarchy as the synchronization source. This section provides information about how to use the export and import functions of the WSUSUtil tool.  

 To export and import software updates metadata, you must export software updates metadata from the WSUS database on a specified export server, then copy the locally stored license terms files to the disconnected software update point, and then import the software updates metadata to the WSUS database on the disconnected software update point.  

 Use the following table to identify the export server in which to export the software updates metadata.  

|Software update point|Upstream update source for connected software update points|Export server for a disconnected software update point|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Central administration site|Microsoft Update (Internet)<br /><br /> Existing WSUS server|Choose a WSUS server that is synchronized with Microsoft Update by using the software update classifications, products, and languages that you need in your Configuration Manager environment.|  
|Stand-alone primary site|Microsoft Update (Internet)<br /><br /> Existing WSUS server|Choose a WSUS server that is synchronized with Microsoft Update by using the software update classifications, products, and languages that you need in your Configuration Manager environment.|  

 Before you start the export process, verify that software updates synchronization is completed on the selected export server to ensure that the most recent software updates metadata is synchronized. To verify that software updates synchronization has completed successfully, use the following procedure.  

##### To verify that software updates synchronization has completed successfully on the export server  

1.  Open the WSUS Administration console and connect to the WSUS database on the export server.  

2.  In the WSUS Administration console, click **Synchronizations**. A list of the software updates synchronization attempts are displayed in the results pane.  

3.  In the results pane, find the latest software updates synchronization attempt and verify that it completed successfully.  

> [!IMPORTANT]  
>  The WSUSUtil tool must be run locally on the export server to export the software updates metadata, and it also must be run on the disconnected software update point server to import the software updates metadata. In addition, the user that runs the WSUSUtil tool must be a member of the local Administrators group on each server.  

#### Export process for software updates  
 The export process for software updates consists of two main steps: to copy the locally stored license terms files to the disconnected software update point, and to export software updates metadata from the WSUS database on the export server.  

 Use the following procedure to copy the local license terms metadata to the disconnected software update point.  

###### To copy local files from the export server to the disconnected software update point server  

1.  On the export server, navigate to the folder where software updates and the license terms for software updates are stored. By default, the WSUS server stores the files at <*WSUSInstallationDrive*>\WSUS\WSUSContent\\, where *WSUSInstallationDrive* is the drive on which WSUS is installed.  

2.  Copy all files and folders from this location to the WSUSContent folder on the disconnected software update point server.  

 Use the following procedure to export the software updates metadata from the WSUS database on the export server.  

###### To export software updates metadata from the WSUS database on the export server  

1.  At the command prompt on the export server, navigate to the folder that contains WSUSutil.exe. By default, the tool is located at %*ProgramFiles*%\Update Services\Tools. For example, if the tool is located in the default location, type **cd %ProgramFiles%\Update Services\Tools**.  

2.  Type the following to export the software updates metadata to a package file:  

     **wsusutil.exe export**  *packagename*  *logfile*  

     For example:  

     **wsusutil.exe export export.cab export.log**  

     The format can be summarized as follows: WSUSutil.exe is followed by the export option, the name of the export .cab file that is created during the export operation, and the name of a log file. WSUSutil.exe exports the metadata from the export server and creates a log file of the operation.  

    > [!NOTE]  
    >  The package (.cab file) and the log file name must be unique in the current folder.  

3.  Move the export package to the folder that contains WSUSutil.exe on the import WSUS server.  

    > [!NOTE]  
    >  If you move the package to this folder, the import experience can be easier. You can move the package to any location that is accessible to the import server, and then specify the location when you run WSUSutil.exe.  

#### Import software updates metadata  
 Use the following procedure to import software updates metadata from the export server to the disconnected software update point.  

> [!IMPORTANT]  
>  Never import any exported data from a source that you do not trust. If you import content from a source that you do not trust, it might compromise the security of your WSUS server.  

###### To import metadata to the database of the import server  

1.  At the command prompt on the import WSUS server, navigate to the folder that contains WSUSutil.exe. By default, the tool is located at %*ProgramFiles*%\Update Services\Tools.  

2.  Type the following:  

     **wsusutil.exe import**  *packagename*  *logfile*  

     For example:  

     **wsusutil.exe import export.cab import.log**  

     The format can be summarized as follows: WSUSutil.exe is followed by the import command, the name of package file (.cab) that is created during the export operation, the path to the package file if it is in a different folder, and the name of a log file. WSUSutil.exe imports the metadata from the export server and creates a log file of the operation.  

## Classifications  
 Configure the classifications settings on the **Classifications** page of the wizard or the on the **Classifications** tab in Software Update Point Component Properties. For more information about software update classifications, see [Update classifications](../../sum/plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  The **Classifications** page of the wizard is available only when you configure the first software update point that you configure on a stand-alone primary site. This page is not displayed when you install additional software update points.  

> [!TIP]  
>  When you first install the software update point on the top-level site, clear all of the software updates classifications. After the initial software updates synchronization, you must configure the classifications from an updated list, and then reinitiate synchronization. This setting is configured only on the software update point at the top-level site.  

## Products  
 Configure the product settings on the **Products** page of the wizard or the on the **Products** tab in Software Update Point Component Properties.  

> [!NOTE]  
>  The **Products** page of the wizard is available only when you configure the first software update point that you configure on a stand-alone primary site. This page is not displayed when you install additional software update points.  

> [!TIP]  
>  When you first install the software update point on the top-level site, clear all of the products. After the initial software updates synchronization, you must configure the products from an updated list, and then reinitiate synchronization. This setting is configured only on the software update point at the top-level site.  

##  <a name="BKMK_ConfigureClassesProducts"></a> Step 3: Configure classifications and products to synchronize  

> [!NOTE]  
>  Use the procedure from this section only on the top-level site.  

 In Step 1, you cleared the list classifications and products. In Step 2, you initiated software update synchronization to update the list of classifications and products in Configuration Manager and WSUS. In step 3, you must select the classifications and products to synchronize.  

 Use the following procedure to configure classifications and products to synchronize.  

#### To configure classifications and products to synchronize  

1.  In the **Configuration Manager** console, click **Administration**.  

2.  In the Administration workspace, expand **Site Configuration**, click **Sites**, and then select the central administration site or stand-alone primary site.  

3.  On the **Home** tab, in the **Settings** group, click **Configure Site Components**, and then click **Software Update Point**.  

4.  On the **Classifications** tab, specify the software update classifications for which you want to synchronize software updates.  

    > [!NOTE]  
    >  Every software update is defined with an update classification that helps to organize the different types of updates. During the synchronization process, the software updates metadata for the specified classifications are synchronized. Configuration Manager provides the ability to synchronize software updates with the following update classifications:  
    >   
    >  -   Critical Updates: Specifies a broadly released update for a specific problem that addresses a critical, non-security-related bug.  
    > -   Definition Updates: Specifies an update to virus or other definition files.  
    > -   Feature Packs: Specifies new product features that are distributed outside of a product release and that are typically included in the next full product release.  
    > -   Security Updates: Specifies a broadly released update for a product-specific, security-related issue.  
    > -   Service Packs: Specifies a cumulative set of hotfixes that are applied to an application. These hotfixes can include: security updates, critical updates, software updates, and so on.  
    > -   Tools: Specifies a utility or feature that helps to complete one or more tasks.  
    > -   Update Rollups: Specifies a cumulative set of hotfixes that are packaged together for easy deployment. These hotfixes can include security updates, critical updates, updates, and so on. An update rollup generally addresses a specific area, such as security or a product component.  
    > -   Updates: Specifies an update to an application or file that is currently installed.  
    > -   Upgrade: Specifies an  upgrade for Windows 10 features and functionality.  
    >   
    >      Your software update points and sites  must run WSUS 4.0 with the [hotfix 3095113](https://support.microsoft.com/kb/3095113) to get the Upgrade classification.  

5.  On the **Products** tab, specify the products for which you want to synchronize software updates, and then click **Close**.  

    > [!NOTE]  
    >  The metadata for each software update defines the products for which the update is applicable. A product is a specific edition of an operating system or application, such as Windows Server 2012. A product family is the base operating system or application from which the individual products are derived. An example of a product family is Windows, of which Windows Server 2012 is a member. You can specify a product family or individual products within a product family. The more products that you select, the longer it will take to synchronize software updates.  
    >   
    >  When software updates are applicable to multiple products, and at least one of the products was selected for synchronization, all of the products will appear in the Configuration Manager console even if some products were not selected. For example, if Windows Server 2012 is the only operating system that you selected, and if a software update applies to Windows 8 and Windows Server 2012, both products will be displayed in the Configuration Manager console.  

    > [!IMPORTANT]  
    >  Configuration Manager stores a list of products and product families from which  you can choose when you first install the software update point. Products and product families that are released after Configuration Manager is released might not be available to select until you complete software updates synchronization, which updates the list of available products and product families from which you can choose.  

6.  Repeat [Step 2: Synchronize Software Updates](#BKMK_SUMSync) to manually initiate software updates synchronization.  

##  <a name="BKMK_AssociatedSettings"></a> Step 4: Verify software updates client settings and group policy configurations  
 There are client settings and group policy configurations that you must verify before you deploy software updates.  

###  <a name="BKMK_ClientSettings"></a> Client settings for software updates  
 After you install the software update point, software updates is enabled on clients by default, and the settings on the **Software Updates** page in client settings have default values. Before you deploy software updates, verify that the client settings on this page is appropriate for the software updates at your site.  

> [!IMPORTANT]  
>  The **Enable software updates on clients** setting is enabled by default. If you clear this setting, Configuration Manager removes the existing deployment policies from the client.  

 For information about how to configure client settings, see [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

 For more information about the client settings, see [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

###  <a name="BKMK_GroupPolicy"></a> Group policy settings for software updates  
 There are specific group policy settings that are used by Windows Update Agent (WUA) on client computers to connect to WSUS that runs on the software updates point. These group policy settings are also used to successfully scan for software update compliance, and to automatically update the software updates and the WUA.  

#### Specify Intranet Microsoft Update Service Location local policy  
 When the software update point is created for a site, clients receive a machine policy that provides the software update point server name and configures the **Specify intranet Microsoft update service location** local policy on the computer. The WUA retrieves the server name that is specified in the **Set the intranet update service for detecting updates** setting, and then it connects to this server when it scans for software updates compliance. When a domain policy is created for the **Specify intranet Microsoft update service location** setting, it overrides the local policy, and the WUA might connect to a server other than the software update point. If this happens, the client might scan for software update compliance based on different products, classifications, and languages. Therefore, you should not configure the Active Directory policy for client computers.  

#### Allow Signed Content from Intranet Microsoft Update Service Location group policy  
 You must enable the **Allow signed content from intranet Microsoft update service location** Group Policy setting before the WUA on computers will scan for software updates that were created and published with System Center Updates Publisher. When the policy setting is enabled, WUA will accept software updates that are received through an intranet location if the software updates are signed in the **Trusted Publishers** certificate store on the local computer. For more information about the Group Policy settings that are required for Updates Publisher, see [Updates Publisher 2011 Documentation Library](http://go.microsoft.com/fwlink/p/?LinkId=232476).  

#### Automatic updates configuration  
 Automatic Updates allows security updates and other important downloads to be received on client computers. Automatic Updates is configured through the **Configure Automatic Updates** Group Policy setting or through the Control Panel on the local computer. When Automatic Updates is enabled, client computers will receive update notifications and, depending on the configured settings, the client computers will download and install the required updates. When Automatic Updates coexists with software updates, each client computer might display notification icons and popup display notifications for the same update. Also, when a restart is required, each client computer might display a restart dialog box for the same update.  

#### Self Update  
 When Automatic Updates is enabled on client computers, the WUA automatically performs a self-update when a newer version becomes available or when there are problems with a WUA component. When Automatic Updates is not configured or is disabled, and client computers have an earlier version of the WUA, the client computers must run the WUA installation file.  

##  <a name="BKMK_RemoveSUP"></a> Remove the software update point site system role  
 You can remove the software update point site system role at a site from the Configuration Manager console. The client policy is updated to remove the software update point from the list. When you remove the last software update point at the site, the software update point list will contain no software update points, and software updates is essentially disabled at the site. When you have more than one software update point at a primary site and you remove the software update point that is configured as the synchronization source, you must choose another software update point at the site to be the new synchronization source.  

> [!NOTE]  
>  When you remove the software update point site role from a site system, wait at least 15 minutes before you reinstall the software update point site role.  

 Use the following procedure to remove a software update point.  

#### To remove the software update point  

1.  In the **Configuration Manager** console, click **Administration**.  

2.  In the Administration workspace, expand **Site Configuration**, and then click **Servers and Site System Roles**.  

3.  Select the site system server with the software update point to remove, and then in **Site System Roles**, select **Software update point**.  

4.  On the **Site Role** tab, in the **Site Role** group, click **Remove Role**. Confirm that you want to remove the software update point or select a new synchronization source for the other software update points at the site.  

## See Also  
 [Deploy and manage software updates in System Center Configuration Manager](../Topic/Deploy%20and%20manage%20software%20updates%20in%20System%20Center%20Configuration%20Manager.md)
