---
title: "Manage software updates in System Center Configuration Manager"
ms.custom: na
ms.date: 2016-07-27
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-sum
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70f66926-c067-404d-94f1-3ad1309566a6
caps.latest.revision: 17
author: Dougeby
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Manage software updates in System Center Configuration Manager
The overall process for software updates in System Center Configuration Manager includes four main operational phases: synchronization, compliance assessment, deployment, and monitoring. The synchronization phase is the process of synchronizing the software update metadata from Microsoft Update and inserting it into the site server database. The compliance assessment phase is the process that client computers perform to scan for compliance of software updates and report the compliance state for the software updates. The deployment phase is the process of manually or automatically deploying the software updates to clients. Finally, the monitoring phase is the process of follow-on monitoring for software update deployment compliance.  
  
> [!IMPORTANT]  
>  Before software update compliance assessment data is displayed in the Configuration Manager console and before you can deploy the software updates to clients, you must carefully plan for the software updates in your hierarchy and configure the software update dependencies to meet the needs of your environment. For more information about planning for software updates, see [Plan for software updates in System Center Configuration Manager](../../sup/plan-design/plan-for-software-updates.md). For more information about configuring software updates, see [Configure software updates in System Center Configuration Manager](../../sup/deploy-use/configure-software-updates.md).  
  
 The following sections in this topic will help you with the operational phases for software updates in Configuration Manager:  
  
-   [Synchronize software updates](#BKMK_SUMSync)  
  
-   [Download software updates](#BKMK_DownloadUpdates)  
  
-   [Manage software update settings](#BKMK_ManageSUSettings)  
  
    -   [Review software updates information](#BKMK_SoftwareUpdatesInformation)  
  
        -   [Software update details](#BKMK_SoftwareUpdateDetails)  
  
        -   [Content information](#BKMK_ContentInformation)  
  
        -   [Custom bundle information](#BKMK_CustomBundleInformation)  
  
        -   [Supersedence information](#BKMK_SupersedenceInformation)  
  
    -   [Configure software updates settings](#BKMK_SoftwareUpdatesSettings)  
  
        -   [Set maximum run time](#BKMK_SetMaxRunTime)  
  
        -   [Set custom severity](#BKMK_SetCustomSeverity)  
  
-   [Add software updates to an update group](#BKMK_AddUpdatesToGroup)  
  
-   [Deploy software updates](#BKMK_SUMDeploy)  
  
    -   [Manually deploy software updates](#BKMK_ManualDeploy)  
  
        -   [Step 1: Specify search criteria for software updates](#BKMK_1SearchCriteria)  
  
        -   [Step 2: Create a software update group that contains the software updates](#BKMK_2UpdateGroup)  
  
        -   [Step 3: Download the content for the software update group](#BKMK_3DownloadContent)  
  
        -   [Step 4: Deploy the software update group](#BKMK_4DeployUpdateGroup)  
  
    -   [Automatically deploy software updates](#BKMK_AutoDeploy)  
  
        -   [Add software updates to an update group](#BKMK_AddUpdatesToGroup)  
  
        -   [Create an automatic deployment rule (ADR)](#BKMK_CreateAutomaticDeploymentRule)  
  
            -   [Add a new deployment to an existing ADR](#BKMK_AddDeploymentToADR)  
  
-   [Schedule and run the WSUS clean up task](#BKMK_WSUSCleanUp)  
  
##  <a name="BKMK_SUMSync"></a> Synchronize software updates  
 Software update synchronization in Configuration Manager is the process of retrieving the software update metadata that meets the criteria that you configure. The software update point on the central administration site, or on a stand-alone primary site, retrieves the metadata from Microsoft Update on a predetermined schedule. Alternatively, you can manually initiate metadata synchronization from the Configuration Manager console. After the software update synchronization is complete at a central administration site, the site sends the child primary sites a synchronization request that instructs them to initiate synchronization. For more information about software update synchronization, see [Software updates synchronization](../../sup/understand/software-updates-introduction.md#BKMK_Synchronization).  
  
 You configure software update synchronization to run on a schedule as part of the properties for the software update point on the top-level site. After you configure the synchronization schedule you will typically not change the schedule as part of normal operations. However, you can manually initiate software update synchronization when it is necessary. For information about configuring the software update synchronization schedule, see [Step 2: Synchronize Software Updates](../../sup/deploy-use/configure-software-updates.md#BKMK_SUMSync).  
  
 Use the following procedure to manually initiate software update synchronization.  
  
#### To manually initiate software updates synchronization on the central administration site  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and click **All Software Updates** or **Software Update Groups**.  
  
3.  On the **Home** tab, in the **Create** group, click **Synchronize Software Updates**. Click **Yes** to confirm that you want to initiate the synchronization process.  
  
 After you initiate the synchronization process, you can use the Configuration Manager console to monitor the process for all software update points in your hierarchy. Use the following procedure to monitor the software update synchronization process.  
  
#### To monitor the software update synchronization process  
  
1.  In the Configuration Manager console, click **Monitoring**.  
  
2.  In the Monitoring workspace, click **Software Update Point Synchronization Status**.  
  
     The results pane displays the software update points in your Configuration Manager hierarchy. From this view, you can monitor the synchronization status for all software update points. To obtain more detailed information about the synchronization process, review the wsyncmgr.log file, which is located in <*ConfigMgrInstallationPath*>\Logs on each site server.  
  
##  <a name="BKMK_DownloadUpdates"></a> Download software updates  
 There are several methods available to you for downloading software updates in Configuration Manager. When you create an automatic deployment rule (ADR) or manually deploy software updates, the software updates are downloaded to the content library on the site server, and then copied to the content library on the distribution points that are associated with the configured deployment package. If you want to download the software updates before you deploy them, you can use the Download Updates Wizard. Doing this will enable you to verify that the software updates are available on distribution points before you deploy the software updates to client computers.  
  
> [!NOTE]  
>  For information about monitoring content status, see the [Content status monitoring](../../sup/deploy-use/monitor-software-updates.md#BKMK_ContentStatus).  
  
 Use the following procedure to download software updates by using the Download Software Updates Wizard.  
  
#### To download software updates  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, click **Software Updates**.  
  
3.  Choose the software update to download by using one of the following methods:  
  
    -   Select one or more software update groups from **Software Update Groups**, and then, on the **Home** tab, in the **Update Group** group, click **Download**.  
  
    -   Select one or more software updates from **All Software Updates**, and then, on the **Home** tab, in the **Update** group, click **Download**.  
  
        > [!NOTE]  
        >  On the **All Software Updates** node, Configuration Manager displays only software updates with a **Critical** and **Security** classification that have been released in the last 30 days.  
  
        > [!TIP]  
        >  Click **Add Criteria** to filter the software updates that are displayed in the **All Software Updates** node, save search criteria that you often use, and then manage saved searches on the **Search** tab.  
  
         The **Download Software Updates Wizard** opens.  
  
4.  On the Deployment Package page, configure the following settings:  
  
    1.  **Select deployment package**: Choose this setting to select an existing deployment package for the software updates that are in the deployment.  
  
        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package will not be downloaded again.  
  
    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates that are in the deployment. Configure the following settings:  
  
        -   **Name**: Specifies the name of the deployment package. The package must have a unique name that briefly describes the package content.  It is limited to 50 characters.  
  
        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  
  
        -   **Package source**: Specifies the location of the software update source files. Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  
  
            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  
  
            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  
  
            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  
  
     Click **Next**.  
  
5.  On the Distribution Points page, specify the distribution points or distribution point groups that will host the software update files, and then click **Next**. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  
  
    > [!NOTE]  
    >  The Distribution Points page is available only when you create a new software update deployment package.  
  
6.  On the Distribution Settings page, specify the following settings:  
  
    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Deployment packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  
  
    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  
  
    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  
  
        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  
  
        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  
  
        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  
  
         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  
  
     Click **Next**.  
  
7.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  
  
    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  
  
    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  
  
        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  
  
     Click **Next**.  
  
8.  On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  
  
9. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  
  
10. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**.  
  
##  <a name="BKMK_ManageSUSettings"></a> Manage software update settings  
 The software update properties provide information about software updates and associated content. You can also use these properties to configure settings for software updates. When you open the properties for multiple software updates, only the **Maximum Run Time** and **Custom Severity** tabs are displayed. The **NAP Evaluation** tab is also displayed if all selected software updates have been downloaded.  
  
 Use the following procedure to open software update properties.  
  
#### To open software update properties  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and click **All Software Updates**.  
  
3.  Select one or more software updates, and then, on the **Home** tab, click **Properties** in the **Properties** group.  
  
    > [!NOTE]  
    >  On the **All Software Updates** node, Configuration Manager displays only the software updates that have a **Critical** and **Security** classification and that have been released in the last 30 days.  
  
###  <a name="BKMK_SoftwareUpdatesInformation"></a> Review software updates information  
 In software update properties, you can review detailed information about a software update. The detailed information is not displayed when you select more than one software update. The following sections describe the information that is available for a selected software update.  
  
####  <a name="BKMK_SoftwareUpdateDetails"></a> Software update details  
 In the **Update Details** tab, you can view the following summary information about the selected software update:  
  
-   **Bulletin ID**: Specifies the bulletin ID that is associated with security software updates. You can find security bulletin details by searching on the bulletin ID at the [Microsoft Security Bulletin Search](http://go.microsoft.com/fwlink/p/?LinkId=58313) Web page.  
  
-   **Article ID**: Specifies the article ID for the software update. The referenced article provides more detailed information about the software update and the issue that the software update fixes or improves.  
  
-   **Date revised**: Specifies the date that the software update was last modified.  
  
-   **Maximum severity rating**: Specifies the vendor-defined severity rating for the software update.  
  
-   **Description**: Provides an overview of what condition the software update fixes or improves.  
  
-   **Applicable languages**: Lists the languages for which the software update is applicable.  
  
-   **Affected products**: Lists the products for which the software update is applicable.  
  
####  <a name="BKMK_ContentInformation"></a> Content information  
 In the **Content Information** tab, review the following information about the content that is associated with the selected software update:  
  
-   **Content ID**: Specifies the content ID for the software update.  
  
-   **Downloaded**: Indicates whether Configuration Manager has downloaded the software update files.  
  
-   **Language**: Specifies the languages for the software update.  
  
-   **Source Path**: Specifies the path to the software update source files.  
  
-   **Size (MB)**: Specifies the size of the software update source files.  
  
####  <a name="BKMK_CustomBundleInformation"></a> Custom bundle information  
 In the **Custom Bundle Information** tab, review the custom bundle information for the software update. When the selected software update contains bundled software updates that are contained in the software update file, they are displayed in the **Bundle information** section. This tab does not display bundled software updates that are displayed in the **Content Information** tab, such as update files for different languages.  
  
####  <a name="BKMK_SupersedenceInformation"></a> Supersedence information  
 On the **Supersedence Information** tab, you can view the following information about the supersedence of the software update:  
  
-   **This update has been superseded by the following updates**: Specifies the software updates that supersede this update, which means that the updates listed are newer. In most cases, you will deploy one of the software updates that supersedes the software update. The software updates that are displayed in the list contain hyperlinks to webpages that provide more information about the software updates. When this update is not superseded, **None** is displayed.  
  
-   **This update supersedes the following updates**: Specifies the software updates that are superseded by this software update, which means this software update is newer. In most cases, you will deploy this software update to replace the superseded software updates. The software updates that are displayed in the list contain hyperlinks to web pages that provide more information about the software updates. When this update does not supersede any other update, **None** is displayed.  
  
###  <a name="BKMK_SoftwareUpdatesSettings"></a> Configure software updates settings  
 In the properties, you can configure software update settings for one or more software updates. You can configure most software update settings only at the central administration site or stand-alone primary site. The following sections will help you to configure settings for software updates.  
  
####  <a name="BKMK_SetMaxRunTime"></a> Set maximum run time  
 In the **Maximum Run Time** tab, set the maximum amount of time a software update is allotted to complete on client computers. If the update takes longer than the maximum run-time value, Configuration Manager creates a status message and stops monitoring the deployment for the software updates installation. You can configure this setting only on the central administration site or a stand-alone primary site.  
  
 Configuration Manager also uses this setting to determine whether to initiate the software update installation within a configured maintenance window. If the maximum run-time value is greater than the available remaining time in the maintenance window, the software updates installation is postponed until the start of the next maintenance window. When there are multiple software updates to be installed on a client computer with a configured maintenance window (timeframe), the software update with the lowest maximum run time installs first, then the software update with the next lowest maximum run time installs next, and so on. Before it installs each software update, the client verifies that the available maintenance window will provide enough time to install the software update. After a software update starts installing, it will continue to install even if the installation goes beyond the end of the maintenance window. For more information about maintenance windows, see the [How to use maintenance windows in System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  
  
 On the **Maximum Run Time** tab, you can view and configure the following settings:  
  
-   **Maximum run time**: Specifies the maximum number of minutes allotted for a software update installation to complete before the installation is no longer monitored by Configuration Manager. This setting is also used to determine whether there is enough available time remaining to install the update before the end of a maintenance window. The default setting is 60 minutes for service packs and 5 minutes for all other software update types. Values can range from 5 to 9999 minutes.  
  
> [!IMPORTANT]  
>  Be sure to set the maximum run time value smaller than the configured maintenance window time. Otherwise, the software update installation will never initiate.  
  
####  <a name="BKMK_SetCustomSeverity"></a> Set custom severity  
 In the properties for a software update, you can use the **Custom Severity** tab to configure custom severity values for the software updates. This may be necessary if the predefined severity values do not meet your needs. The custom values are listed in the **Custom Severity** column in the Configuration Manager console. You can sort the software updates by the defined custom severity values and can also create queries and reports that can filter on these values. You can configure this setting only on the central administration site or stand-alone primary site.  
  
 You can configure the following settings on the **Custom Severity** tab.  
  
-   **Custom severity**: Sets a custom severity value for the software updates. Select **Critical**, **Important**, **Moderate**, or **Low** from the list. By default, the custom severity value is empty.  
  
##  <a name="BKMK_AddUpdatesToGroup"></a> Add software updates to an update group  
 Software update groups provide you with an effective method to organize software updates in your environment. You can manually add software updates to a software update group or automatically add software updates to a software update group by using an ADR. You can also deploy a software update group manually or deploy the group automatically by using an ADR. After you deploy a software update group, you can add new software updates to the group and Configuration Manager will automatically deploy them. Use the following procedures to add software updates to a new or existing software update group.  
  
#### To add software updates to a new software update group  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and then click **All Software Updates**.  
  
3.  Select the software updates to be added to the new software update group.  
  
4.  On the **Home** tab, in the **Update** group, click **Create Software Update Group**.  
  
5.  Specify the name for the software update group and optionally provide a description. Use a name and description that provide enough information for you to determine what type of software updates are in the software update group. To proceed, click **Create**.  
  
6.  Click **Software Update Groups** to display the new software update group.  
  
7.  Select the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates that are included in the group.  
  
#### To add software updates to an existing software update group  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and then click **All Software Updates**.  
  
3.  Select the software updates that you want to add to the new software update group.  
  
    > [!NOTE]  
    >  On the **All Software Updates** node, by default, Configuration Manager displays only software updates with a **Critical** and **Security** classification and that were released in the last 30 days.  
  
4.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  
  
5.  Select the software update group into which you want to add the software updates.  
  
6.  Click the **Software Update Groups** node to display the software update group.  
  
7.  Select the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates that are included in the software update group.  
  
##  <a name="BKMK_SUMDeploy"></a> Deploy software updates  
 The software update deployment phase is the process of deploying the software updates. Typically, you add software updates to a software update group and then deploy the software update group to clients. When you create the deployment, the software update policy is sent to client computers, the software update content files are downloaded from a distribution point to the local cache on the client computer, and then the software updates are available for installation on the client. Clients on the Internet download content from Microsoft Update.  
  
> [!NOTE]  
>  You can configure a client on the intranet to download software updates from Microsoft Update if a distribution point is not available.  
  
> [!NOTE]  
>  Unlike other deployment types, software updates are all downloaded to the client cache regardless of the maximum cache size setting on the client. For more information about the client cache setting, see [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  
  
 If you configure a required software update deployment, the software updates are automatically installed at the scheduled deadline. Alternatively, the user on the client computer can schedule or initiate the software update installation prior to the deadline. After the attempted installation, client computers send state messages back to the site server to report whether the software update installation was successful. For more information about software update deployments, see [Software update deployment workflows](../../sup/understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  
  
 There are two main scenarios for deploying software updates: manual deployment and automatic deployment. Typically, you will initially manually deploy software updates to create a baseline for your client computers, and then you will manage software updates on clients by using automatic deployment.  
  
 The following sections provide information and procedures for manual and automatic deployment workflows for software updates.  
  
###  <a name="BKMK_ManualDeploy"></a> Manually deploy software updates  
 A manual software update deployment is the process of selecting software updates from the Configuration Manager console and manually initiating the deployment process. Or, you can add selected software updates to an update group, and then manually deploy the update group. You will typically use manual deployment to get your client devices up-to-date with required software updates before you create ADRs that will manage ongoing monthly software update deployments. You will also use a manual method to deploy out-of-band software updates. The following sections provide the general workflow for manual deployment of software updates.  
  
####  <a name="BKMK_1SearchCriteria"></a> Step 1: Specify search criteria for software updates  
 There are potentially thousands of software updates displayed in the Configuration Manager console. The first step in the workflow for manually deploying software updates is to identify the software updates that you want to deploy. For example, you could provide criteria that retrieves all software updates that are required on more than 50 client devices and that have a **Security** or **Critical** software update classification.  
  
> [!IMPORTANT]  
>  The maximum number of software updates that can be included in a single software update deployment is 1000.  
  
###### To specify search criteria for software updates  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and click **All Software Updates**. The synchronized software updates are displayed.  
  
    > [!NOTE]  
    >  On the **All Software Updates** node, Configuration Manager displays only software updates with a **Critical** and **Security** classification and have been released in the last 30 days.  
  
3.  In the search pane, filter to identify the software updates that you need by using one or both of the following steps:  
  
    -   In the search text box, type a search string that will filter the software updates. For example, type the article ID or bulletin ID for a specific software update, or enter a string that would appear in the title for several software updates.  
  
    -   Click **Add Criteria**, select the criteria that you want to use to filter software updates, click **Add**, and then provide the values for the criteria.  
  
4.  Click **Search** to filter the software updates.  
  
    > [!TIP]  
    >  You have the option to save the filter criteria on the **Search** tab and in the **Save** group.  
  
####  <a name="BKMK_2UpdateGroup"></a> Step 2: Create a software update group that contains the software updates  
 Software update groups provide an effective method for you to organize software updates in preparation for deployment. You can manually add software updates to a software update group or Configuration Manager can automatically add software updates to a new or existing software update group by using an ADR. Use the following procedures to manually add software updates to a new software update group.  
  
###### To manually add software updates to a new software update group  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, click **Software Updates**.  
  
3.  Select the software updates that are to be added to the new software update group.  
  
4.  On the **Home** tab, in the **Update** group, click **Create Software Update Group**.  
  
5.  Specify the name for the software update group and optionally provide a description. Use a name and description that provide enough information for you to determine what type of software updates are in the software update group. To proceed, click **Create**.  
  
6.  Click the **Software Update Groups** node to display the new software update group.  
  
7.  Select the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates that are included in the group.  
  
####  <a name="BKMK_3DownloadContent"></a> Step 3: Download the content for the software update group  
 Optionally, before you deploy the software updates, you can download the content for the software updates that are included in the software update group. You might choose to do this so you can verify that the content is available on the distribution points before you deploy the software updates. This will help you to avoid any unexpected issues with the content delivery. You can skip this step and the content will be downloaded and copied to the distribution points as part of the deployment process. Use the following procedure to download the content for software updates in the software update group.  
  
###### To download content for the software update group  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  
  
3.  Select the software update group for which you want to download content.  
  
4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  
  
5.  On the **Deployment Package** page, configure the following settings:  
  
    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  
  
        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  
  
    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  
  
        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  
  
        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  
  
        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  
  
            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  
  
            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  
  
            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  
  
     Click **Next**.  
  
6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  
  
7.  On the Distribution Settings page, specify the following settings:  
  
    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  
  
    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  
  
    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  
  
        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  
  
        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  
  
        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  
  
         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  
  
     Click **Next**.  
  
8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  
  
    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  
  
    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  
  
        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  
  
     Click **Next**.  
  
9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  
  
10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  
  
11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**.  
  
12. To monitor the content status for the software updates, click **Monitoring** in the Configuration Manager console.  
  
13. In the Monitoring workspace, expand **Distribution Status**, and then click **Content Status**.  
  
14. Select the software update package that you previously identified to download the software updates in the software update group.  
  
15. On the **Home** tab, in the **Content** group, click **View Status**.  
  
####  <a name="BKMK_4DeployUpdateGroup"></a> Step 4: Deploy the software update group  
 After you determine which software updates you intend to deploy and add these software updates to a software update group, you can manually deploy the software updates in the software update group. Use the following procedure to manually deploy the software updates in a software update group.  
  
###### To manually deploy the software updates in a software update group  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  
  
3.  Select the software update group that you intend to deploy.  
  
4.  On the **Home** tab, in the **Deployment** group, click **Deploy**. The **Deploy Software Updates Wizard** opens.  
  
5.  On the General page, configure the following settings:  
  
    -   **Name**: Specify the name for the deployment. The deployment must have a unique name that describes the purpose of the deployment, and differentiates it from other deployments in the Configuration Manager site. By default, Configuration Manager automatically provides a name for the deployment in the following format: **Microsoft Software Updates -** <*date*><*time*>  
  
    -   **Description**: Specify a description for the deployment. The description provides an overview of the deployment and any other relevant information that helps to identify and differentiate the deployment among others in Configuration Manager site. The description field is optional, has a limit of 256 characters, and has a blank value by default.  
  
    -   **Software Update/Software Update Group**: Verify that the displayed software update group, or software update, is correct.  
  
    -   **Select Deployment Template**: Specify whether to apply a previously saved deployment template. You can configure a deployment template to contain  multiple common software update deployment properties and then apply the template when you deploy subsequent software updates to ensure consistency across similar deployments and to save time.  
  
    -   **Collection**: Specify the collection for the deployment, as applicable. Members of the collection receive the software updates that are defined in the deployment.  
  
6.  On the Deployment Settings page, configure the following settings:  
  
    -   **Type of deployment**: Specify the deployment type for the software update deployment. Select **Required** to create a mandatory software update deployment in which the software updates are automatically installed on clients before a configured installation deadline. Select **Available** to create an optional software update deployment that is available for users to install from Software Center.  
  
        > [!IMPORTANT]  
        >  After you create the software update deployment, you cannot later change the type of deployment.  
  
        > [!NOTE]  
        >  A software update group deployed as **Required** will be downloaded in background and honor  BITS settings, if configured.  
        > However, software update groups deployed as **Available** will be downloaded in the foreground and will ignore BITS settings.  
  
    -   **Use Wake-on-LAN to wake up clients for required deployments**: Specify whether to enable Wake On LAN at the deadline to send wake-up packets to computers that require one or more software updates in the deployment. Any computers that are in sleep mode at the installation deadline time will be awakened  so the software update installation can initiate. Clients that are in sleep mode that do not require any software updates in the deployment are not started. By default, this setting is not enabled and is available only when **Type of deployment** is set to **Required**.  
  
        > [!WARNING]  
        >  Before you can use this option, computers and networks must be configured for Wake On LAN.  
  
    -   **Detail level**: Specify the level of detail for the state messages that are reported by client computers.  
  
7.  On the Scheduling page, configure the following settings:  
  
    -   **Schedule evaluation**: Specify whether the available time and installation deadline times are evaluated according to UTC or the local time of the computer running the Configuration Manager console.  
  
        > [!NOTE]  
        >  When you select local time, and then select **As soon as possible** for the **Software available time** or **Installation deadline**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available or when they are installed on a client. If the client is in a different time zone, these actions will occur when the client's time reaches the evaluation time.  
  
    -   **Software available time**: Select one of the following settings to specify when the software updates will be available to clients:  
  
        -   **As soon as possible**: Select this setting to make the software updates in the deployment available to clients as soon as possible. When the deployment is created, the client policy is updated, the clients are made aware of the deployment at their next client policy polling cycle, and then the software updates are available for installation.  
  
        -   **Specific time**: Select this setting to make the software updates in the deployment available to clients at a specific date and time. When the deployment is created, the client policy is updated and clients are made aware of the deployment at their next client policy polling cycle. However, the software updates in the deployment are not available for installation until after the specified date and time.  
  
    -   **Installation deadline**: Select one of the following settings to specify the installation deadline for the software updates in the deployment.  
  
        > [!NOTE]  
        >  You can configure the installation deadline setting only when **Type of deployment** is set to **Required** on the Deployment Settings page.  
  
        -   **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.  
  
        -   **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time.  
  
        > [!NOTE]  
        >  The actual installation deadline time is the specific time that you configure plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the software updates in the deployment at the same time.  
        >   
        >  You can configure the **Computer Agent** client setting, **Disable deadline randomization** to disable the installation randomization delay for the required software updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#BKMK_ComputerAgentDeviceSettings).  
  
8.  On the User Experience page, configure the following settings:  
  
    -   **User notifications**: Specify whether to display notification of the software updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers. When **Type of deployment** is set to **Available** on the Deployment Settings page, you cannot select **Hide in Software Center and all notifications**.  
  
    -   **Deadline behavior**: Specify the behavior that is to occur when the deadline is reached for the software update deployment. Specify whether to install the software updates in the deployment. Also specify whether to perform a system restart after software update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  
  
    -   **Device restart behavior**: Specify whether to suppress a system restart on servers and workstations after software updates are installed and a system restart is required to complete the installation.  
  
        > [!IMPORTANT]  
        >  Suppressing system restarts can be useful in server environments or for cases in which you do not want the computers that are installing the software updates to restart by default. However, doing so can leave computers in an insecure state, whereas allowing a forced restart helps to ensure immediate completion of the software update installation. .  
  
    -   **Write filter handling for Windows Embedded devices**: When you deploy software updates to Windows Embedded devices that are write filter enabled, you can specify to install the software update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  
  
        > [!NOTE]  
        >  When you deploy a software update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.  
  
     You can configure the **Deadline behavior** and **Device restart behavior** settings only when **Type of deployment** is set to **Required** on the Deployment Settings page.  
  
9. On the Alerts page, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment. You can configure alerts only when **Type of deployment** is set to **Required** on the Deployment Settings page.  
  
    > [!WARNING]  
    >  You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.  
  
10. On the Download Settings page, configure the following settings:  
  
    -   Specify whether the client will download and install the software updates when a client is connected to a slow network or is using a fallback content location.  
  
    -   Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates is not available on a preferred distribution point.  
  
    -   **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see  [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_Concepts).  
  
    -   Specify whether to have clients that are connected to the intranet download software updates from Microsoft Update if software updates are not available on distribution points.  
  
    -   Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  
  
    > [!NOTE]  
    >  Clients request the content location from a management point for the software updates in a deployment. The download behavior depends upon how you have configured the distribution point, the deployment package, and the settings on this page. For more information, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  
  
11. If you have performed [Step 3: Download the content for the software update group](#BKMK_3DownloadContent), then the Deployment Package, Distribution Points, and Language Selection pages are not displayed, and you can skip to step 15 of the wizard.  
  
    > [!IMPORTANT]  
    >  Software updates that have been previously downloaded to the content library on the site server are not downloaded again. This is true even when you create a new deployment package for the software updates. If all software updates have already been previously downloaded, the wizard skips to the **Language Selection** page (step 15).  
  
12. On the Deployment Package page, select an existing deployment package or configure the following settings to specify a new deployment package:  
  
    1.  **Name**: Specify the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  
  
    2.  **Description**: Specify a description that provides information about the deployment package. The description is limited to 127 characters.  
  
    3.  **Package source**: Specify the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  
  
        > [!NOTE]  
        >  The deployment package source location that you specify cannot be used by another software deployment package.  
  
        > [!IMPORTANT]  
        >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  
  
        > [!IMPORTANT]  
        >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  
  
    4.  **Sending priority**: Specify the sending priority for the deployment package. Configuration Manager uses the sending priority for the deployment package when it sends the package to distribution points. Deployment packages are sent in priority order: High, Medium, or Low. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority.  
  
13. On the Distribution Points page, specify the distribution points or distribution point groups that will host the software update files. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  
  
14. On the Download Location page, specify whether to download the software update files from the Internet or from your local network. Configure the following settings:  
  
    -   **Download software updates from the Internet**: Select this setting to download the software updates from a specified location on the Internet. This setting is enabled by default.  
  
    -   **Download software updates from a location on the local network**: Select this setting to download the software updates from a local folder or shared network folder. This setting is useful when the computer that runs the wizard does not have Internet access. The software updates can be preliminarily downloaded from any computer that has Internet access and stored in a location on the local network for subsequent access for installation.  
  
15. On the Language Selection page, select the languages for which the selected software updates are downloaded. The software updates are downloaded only if they are available in the selected languages. Software updates that are not language specific are always downloaded. By default, the wizard selects the languages that you have configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that are not supported by a software update, the download will fail for the software update.  
  
16. On the Summary page, review the settings. To save the settings to a deployment template, click **Save As Template**, enter a name and select the settings that you want to include in the template, and then click **Save**. To change a configured setting, click the associated wizard page and change the setting.  
  
    > [!WARNING]  
    >  The template name can consist of alphanumeric ASCII characters as well as **\\** (backslash) or **‘** (single quotation mark).  
  
17. Click **Next** to deploy the software update.  
  
 After you have completed the wizard, Configuration Manager downloads the software updates to the content library on the site server, distributes the software updates to the configured distribution points, and then deploys the software update group to clients in the target collection. For more information about the deployment process, see [Software update deployment process](../../sup/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  
  
###  <a name="BKMK_AutoDeploy"></a> Automatically deploy software updates  
 You can automatically deploy software updates by adding new software updates to an update group that has an active deployment or by using ADRs.  
  
####  <a name="BKMK_AddUpdatesToExistingGroup"></a> Add software updates to a deployed update group  
 After you create and deploy a software update group, you can add software updates to the update group and they will also be automatically deployed.  
  
> [!IMPORTANT]  
>  When you add software updates to an existing software update group that has already been deployed, it might take several minutes before the additional software updates are added to the deployment.  
  
 Use the following procedure to add software updates to an existing update group.  
  
###### To add software updates to an existing software update group  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, click **Software Updates**.  
  
3.  Select the software updates that are to be added to the new software update group.  
  
4.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  
  
5.  Select the software update group to which you want to add the software updates as members.  
  
6.  Click the **Software Update Groups** node to display the software update group.  
  
7.  Click the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates in the group.  
  
####  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Create an automatic deployment rule (ADR)  
 You can automatically approve and deploy software updates by using an ADR. This is a common method of deployment for monthly software updates ("Patch Tuesday") and for managing definition updates. When the ADR runs, software updates are removed from the software update group (if using an existing group), the software updates that meet a specified criteria are added to a software update group, the content files for the software updates are downloaded and copied to distribution points, and the software updates are deployed to client devices in the target collection. After you create an ADR, you can add additional deployments to the rule.  
  
 You can have the rule add software updates to a new software update group each time the rule runs or add software updates to an existing group. When a rule runs and adds software updates to an existing group, the rule removes all software updates from the group and then adds the software updates that meet the criteria that you define to the group. To run an ADR to find newly released software updates each day and deploy them to clients, for example, you must choose the option to create a new software update group instead of adding the software updates to an existing group.  
  
> [!WARNING]  
>  Before you create an ADR for the first time, verify that software updates synchronization has completed at the site. This is particularly important when you run Configuration Manager with a non-English language because software update classifications are displayed in English before the first synchronization, and then displayed in the localized language after software update synchronization completes. Rules that you create before you synchronize software updates might not work properly after synchronization because the text string might not match.  
  
 Use the following procedure to create an ADR.  
  
###### To create an ADR  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, and click **Automatic Deployment Rules**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Automatic Deployment Rule**. The Create Automatic Deployment Rule Wizard opens.  
  
4.  On the **General** page, configure the following settings:  
  
    -   **Name**: Specify the name for the ADR. The name must be unique, help to describe the objective of the rule, and identify it from others in the Configuration Manager site.  
  
    -   **Description**: Specify a description for the ADR. The description should provide an overview of the deployment rule and any other relevant information that helps to identify and differentiate the rule among others in the Configuration Manager site. The description field is optional, has a limit of 256 characters, and has a blank value by default.  
  
    -   **Select Deployment Template**: Specify whether to apply a previously saved deployment template. You can configure a deployment template to contain multiple common software update deployment properties that can then be used when creating ADRs. These templates help to ensure consistency across similar deployments and to save time.  
  
         You can select from the built-in software update deployment templates from the Automatic Deployment Rule Wizard. The **Definition Updates** template provides common settings to use when you deploy definition software updates. The **Patch Tuesday** template provides common settings to use when you deploy software updates on a monthly cycle.  
  
    -   **Collection**: Specifies the target collection to be used for the deployment. Members of the collection receive the software updates that are defined in the deployment.  
  
    -   Decide whether to add software updates to a new or existing software update group. In most cases, you will probably choose to create a new software update group when the ADR is run. However, you might choose to use an existing group if the rule runs on a more aggressive schedule. For example, if you will run the rule daily for definition updates, then you could add the software updates to an existing software update group.  
  
    -   **Enable the deployment after this rule is run**: Specify whether to enable the software update deployment after the ADR runs. Regarding this specification, consider the following:  
  
        -   When you enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group, the software update content is downloaded as necessary, the content is copied to the specified distribution points, and the software updates are deployed to the clients in the target collection.  
  
        -   When you do not enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group and the software updates deployment policy is configured but the software updates are not downloaded or deployed to clients. This situation provides you time as needed to prepare to deploy the software updates, verify that the software updates that meet the criteria are adequate, and then enable the deployment at a later time.  
  
5.  On the Deployment Settings page, configure the following settings:  
  
    -   **Use Wake-on-LAN to wake up clients for required deployments**: Specifies whether to enable Wake On LAN at the deadline to send wake-up packets to computers that require one or more software updates in the deployment. Any computers that are in sleep mode at the installation deadline time will be awakened so the software update installation can initiate. Clients that are in sleep mode that do not require any software updates in the deployment are not started. By default, this setting is not enabled.  
  
        > [!WARNING]  
        >  Before you can use this option, you must configure computers and networks for Wake On LAN.  
  
    -   **Detail level**: Specify the level of detail for the state messages that are reported by client computers.  
  
        > [!IMPORTANT]  
        >  When you deploy definition updates, set the detail level to **Error only** to have the client report a state message only when a definition update fails to be delivered to the client. Otherwise, the client will report a large number of state messages that might impact performance on the site server.  
  
    -   **License terms setting**: Specify whether to automatically deploy software updates with associated license terms. Some software updates include license terms, such as a service pack. When you automatically deploy software updates, the license terms are not displayed and there is not an option to accept the license terms. You can choose to automatically deploy all software updates regardless of an associated license terms or only deploy software updates that do not have associated license terms.  
  
        > [!WARNING]  
        >  To review the license terms for a software update, you can select the software update in the **All Software Updates** node of the **Software Library** workspace, and then on the **Home** tab, in the **Update** group, click **Review License**.  
        >   
        >  To find software updates with associated license terms, you can add the **License Terms** column to the results pane in the **All Software Updates** node, and then click the heading for the column to sort by the software updates with license terms.  
  
6.  On the Software Updates page, configure the criteria for the software updates that the ADR retrieves and adds to the software update group.  
  
    > [!IMPORTANT]  
    >  The limit for software updates in the ADR is 1000 software updates. To ensure that the criteria that you specify on this page retrieves less than 1000 software updates, consider setting the same criteria on the **All Software Updates** node in the **Software Library** workspace.  
  
7.  On the Evaluation Schedule page, specify whether to enable the ADR to run on a schedule. When enabled, click **Customize** to set the recurring schedule.  
  
    > [!IMPORTANT]  
    >  The software update point synchronization schedule is displayed to help you determine the frequency of the evaluation schedule. You should never set the evaluation schedule with a frequency that exceeds the software updates synchronization schedule. The start time configuration for the schedule is based on the local time of the computer that runs the Configuration Manager console.  
  
    > [!NOTE]  
    >  To manually run the ADR, select the rule, and then click **Run Now** on the **Home** tab in the **Automatic Deployment Rule** group. Before you manually run the ADR, verify that software updates synchronization has been run since the last time you ran the rule.  
  
    > [!IMPORTANT]  
    >  The ADR evaluation can run as often as three times per day.  
  
8.  On the Deployment Schedule page, configure the following settings:  
  
    -   **Schedule evaluation**: Specify whether Configuration Manager evaluates the available time and installation deadline times by using UTC or the local time of the computer that runs the Configuration Manager console.  
  
        > [!NOTE]  
        >  When you select local time, and then select **As soon as possible** for the **Software available time** or **Installation deadline**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available or when they are installed on a client. If the client is in a different time zone, these actions will occur when the client's time reaches the evaluation time.  
  
    -   **Software available time**: Select one of the following settings to specify when the software updates are available to clients:  
  
        -   **As soon as possible**: Select this setting to make the software updates that are included in the deployment available to the client computers as soon as possible. When you create the deployment with this setting selected, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become  aware of the deployment and can obtain the updates that are available for installation.  
  
        -   **Specific time**: Select this setting to make the software updates that are included in the deployment available to the client computers at a specific date and time. When you create the deployment with this setting enabled, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become aware of the deployment. However, the software updates in the deployment are not available for installation until after the configured date and time.  
  
    -   **Installation deadline**: Select one of the following settings to specify the installation deadline for the software updates in the deployment:  
  
        -   **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.  
  
        -   **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time. Configuration Manager determines the deadline to install software updates by adding the configured **Specific time** interval to the **Software available time**.  
  
        > [!NOTE]  
        >  The actual installation deadline time is the displayed deadline time plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the software updates in the deployment at the same time.  
        >   
        >  You can configure the **Computer Agent** client setting **Disable deadline randomization** to disable the installation randomization delay for required software updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#BKMK_ComputerAgentDeviceSettings).  
  
9. On the User Experience page, configure the following settings:  
  
    -   **User notifications**: Specify whether to display notification of the software updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers.  
  
    -   **Deadline behavior**: Specify the behavior that is to occur when the deadline is reached for the software update deployment. Specify whether to install the software updates in the deployment. Also specify whether to perform a system restart after software update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  
  
    -   **Device restart behavior**: Specify whether to suppress a system restart on servers and workstations after software updates are installed and a system restart is required to complete the installation.  
  
        > [!IMPORTANT]  
        >  Suppressing system restarts can be useful in server environments or in cases in which you do not want the computers that are installing the software updates to restart by default. However, doing so can leave computers in an insecure state, whereas allowing a forced restart helps to ensure immediate completion of the software update installation.  
  
    -   **Write filter handling for Windows Embedded devices**: When you deploy software updates to Windows Embedded devices that are write filter enabled, you can specify to install the software update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  
  
        > [!NOTE]  
        >  When you deploy a software update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.  
  
10. On the Alerts page, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment.  
  
    > [!WARNING]  
    >  You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.  
  
11. On the Download Settings page, configure the following settings:  
  
    -   Specify whether the client will download and install the software updates when a client is connected to a slow network or is using a fallback content location.  
  
    -   Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates is not available on a preferred distribution point.  
  
    -   **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_Concepts).  
  
    -   Specify whether to have clients that are connected to the intranet download software updates from Microsoft Update if software updates are not available on distribution points.  
  
    -   Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  
  
    > [!NOTE]  
    >  Clients request the content location from a management point for the software updates in a deployment. The download behavior depends upon how you have configured the distribution point, deployment package, and the settings on this page. For more information, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  
  
12. On the Deployment Package page, select an existing deployment package or configure the following settings to create a new deployment package:  
  
    1.  **Name**: Specify the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  
  
    2.  **Description**: Specify a description that provides information about the deployment package. The description is limited to 127 characters.  
  
    3.  **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  
  
        > [!NOTE]  
        >  The deployment package source location that you specify cannot be used by another software deployment package.  
  
        > [!IMPORTANT]  
        >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  
  
        > [!IMPORTANT]  
        >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  
  
    4.  **Sending priority**: Specify the sending priority for the deployment package. Configuration Manager uses the sending priority for the deployment package when it sends the package to distribution points. Deployment packages are sent in priority order: High, Medium, or Low. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority.  
  
13. On the Distribution Points page, specify the distribution points or distribution point groups that will host the software update files. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  
  
    > [!NOTE]  
    >  This page is available only when you create a new software update deployment package.  
  
14. On the Download Location page, specify whether to download the software update files from the Internet or from your local network. Configure the following settings:  
  
    -   **Download software updates from the Internet**: Select this setting to download the software updates from a specified location on the Internet. This setting is enabled by default.  
  
    -   **Download software updates from a location on the local network**: Select this setting to download the software updates from a local directory or shared folder. This setting is useful when the computer that runs the wizard does not have Internet access. Any computer with Internet access can preliminarily download the software updates and store them in a location on the local network that is accessible from the computer that runs the wizard.  
  
15. On the Language Selection page, select the languages for which the selected software updates are downloaded. The software updates are downloaded only if they are available in the selected languages. Software updates that are not language specific are always downloaded. By default, the wizard selects the languages that you have configured in the software update point properties. At least one language must be selected before proceeding to the next page. When you select only languages that are not supported by a software update, the download will fail for the software update.  
  
16. On the Summary page, review the settings. To save the settings to a deployment template, click **Save As Template**, enter a name and select the settings that you want to include in the template, and then click **Save**. To change a configured setting, click the associated wizard page and change the setting.  
  
    > [!WARNING]  
    >  The template name can consist of alphanumeric ASCII characters as well as **\\** (backslash) or **‘** (single quotation mark).  
  
17. Click **Next** to create the ADR.  
  
 After you have completed the wizard, the ADR will run. It will add the software updates that meet the specified criteria to a software update group, download the software updates to the content library on the site server, distribute the software updates to the configured distribution points, and then deploy the software update group to clients in the target collection.  
  
#####  <a name="BKMK_AddDeploymentToADR"></a> Add a new deployment to an existing ADR  
 After you create an ADR, you can add additional deployments to the rule. This can help you manage the complexity of deploying different updates to different collections. Each new deployment has the full range of functionality and deployment monitoring experience.  
  
###### To add a new deployment to an existing ADR  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the Software Library workspace, expand **Software Updates**, click **Automatic Deployment Rules**, and then select the desired rule.  
  
3.  On the **Home** tab, in the **Automatic Deployment Rule** group, click **Add Deployment**. The Add Deployment Wizard opens.  
  
4.  On the **Collection** page, configure the following settings:  
  
    -   **Collection**: Specifies the target collection to be used for the deployment. Members of the collection receive the software updates that are defined in the deployment.  
  
    -   **Enable the deployment after this rule is run**: Specify whether to enable the software update deployment after the ADR runs. Regarding this specification, consider the following:  
  
        -   When you enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group, the software update content is downloaded as necessary, the content is copied to the specified distribution points, and the software updates are deployed to the clients in the target collection.  
  
        -   When you do not enable the deployment, the software updates that meet the criteria defined in the rule are added to a software update group and the software updates deployment policy is configured but the software updates are not downloaded or deployed to clients. This situation provides you time as needed to prepare to deploy the software updates, verify that the software updates that meet the criteria are adequate, and then enable the deployment at a later time.  
  
5.  On the Deployment Settings page, configure the following settings:  
  
    -   **Use Wake-on-LAN to wake up clients for required deployments**: Specifies whether to enable Wake On LAN at the deadline to send wake-up packets to computers that require one or more software updates in the deployment. Any computers that are in sleep mode at the installation deadline time will be awakened so the software update installation can initiate. Clients that are in sleep mode that do not require any software updates in the deployment are not started. By default, this setting is not enabled.  
  
        > [!WARNING]  
        >  Before you can use this option, you must configure computers and networks for Wake On LAN.  
  
    -   **Detail level**: Specify the level of detail for the state messages that are reported by client computers.  
  
        > [!IMPORTANT]  
        >  When you deploy definition updates, set the detail level to **Error only** to have the client report a state message only when a definition update fails to be delivered to the client. Otherwise, the client will report a large number of state messages that might impact performance on the site server.  
  
6.  On the Deployment Schedule page, configure the following settings:  
  
    -   **Schedule evaluation**: Specify whether Configuration Manager evaluates the available time and installation deadline times by using UTC or the local time of the computer that runs the Configuration Manager console.  
  
        > [!NOTE]  
        >  When you select local time, and then select **As soon as possible** for the **Software available time** or **Installation deadline**, the current time on the computer running the Configuration Manager console is used to evaluate when updates are available or when they are installed on a client. If the client is in a different time zone, these actions will occur when the client's time reaches the evaluation time.  
  
    -   **Software available time**: Select one of the following settings to specify when the software updates are available to clients:  
  
        -   **As soon as possible**: Select this setting to make the software updates that are included in the deployment available to the client computers as soon as possible. When you create the deployment with this setting selected, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become  aware of the deployment and can obtain the updates that are available for installation.  
  
        -   **Specific time**: Select this setting to make the software updates that are included in the deployment available to the client computers at a specific date and time. When you create the deployment with this setting enabled, Configuration Manager updates the client policy. Then, at the next client policy polling cycle, clients become aware of the deployment. However, the software updates in the deployment are not available for installation until after the configured date and time.  
  
    -   **Installation deadline**: Select one of the following settings to specify the installation deadline for the software updates in the deployment:  
  
        -   **As soon as possible**: Select this setting to automatically install the software updates in the deployment as soon as possible.  
  
        -   **Specific time**: Select this setting to automatically install the software updates in the deployment at a specific date and time. Configuration Manager determines the deadline to install software updates by adding the configured **Specific time** interval to the **Software available time**.  
  
        > [!NOTE]  
        >  The actual installation deadline time is the displayed deadline time plus a random amount of time up to 2 hours. This reduces the potential impact of all client computers in the destination collection installing the software updates in the deployment at the same time.  
        >   
        >  You can configure the **Computer Agent** client setting **Disable deadline randomization** to disable the installation randomization delay for required software updates. For more information, see [Computer Agent](../../core/clients/deploy/about-client-settings.md#BKMK_ComputerAgentDeviceSettings).  
  
7.  On the User Experience page, configure the following settings:  
  
    -   **User notifications**: Specify whether to display notification of the software updates in Software Center on the client computer at the configured **Software available time** and whether to display user notifications on the client computers.  
  
    -   **Deadline behavior**: Specify the behavior that is to occur when the deadline is reached for the software update deployment. Specify whether to install the software updates in the deployment. Also specify whether to perform a system restart after software update installation regardless of a configured maintenance window. For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  
  
    -   **Device restart behavior**: Specify whether to suppress a system restart on servers and workstations after software updates are installed and a system restart is required to complete the installation.  
  
        > [!IMPORTANT]  
        >  Suppressing system restarts can be useful in server environments or in cases in which you do not want the computers that are installing the software updates to restart by default. However, doing so can leave computers in an insecure state, whereas allowing a forced restart helps to ensure immediate completion of the software update installation.  
  
    -   **Write filter handling for Windows Embedded devices**: When you deploy software updates to Windows Embedded devices that are write filter enabled, you can specify to install the software update on the temporary overlay and either commit changes later or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  
  
        > [!NOTE]  
        >  When you deploy a software update to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window.  
  
8.  On the Alerts page, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment.  
  
    > [!WARNING]  
    >  You can review recent software updates alerts from the **Software Updates** node in the **Software Library** workspace.  
  
9. On the Download Settings page, configure the following settings:  
  
    -   Specify whether the client will download and install the software updates when a client is connected to a slow network or is using a fallback content location.  
  
    -   Specify whether to have the client download and install the software updates from a fallback distribution point when the content for the software updates is not available on a preferred distribution point.  
  
    -   **Allow clients to share content with other clients on the same subnet**: Specify whether to enable the use of BranchCache for content downloads. For more information about BranchCache, see [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_Concepts).  
  
    -   Specify whether to have clients that are connected to the intranet download software updates from Microsoft Update if software updates are not available on distribution points.  
  
    -   Specify whether to allow clients to download after an installation deadline when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  
  
    > [!NOTE]  
    >  Clients request the content location from a management point for the software updates in a deployment. The download behavior depends upon how you have configured the distribution point, deployment package, and the settings on this page. For more information, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  
  
 For more information about the deployment process, see [Software update deployment process](../../sup/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  
  
##  <a name="BKMK_WSUSCleanUp"></a> Schedule and run the WSUS clean up task  
 You can schedule and run the WSUS clean up task from the Configuration Manager console.  
You can manually run the WSUS cleanup task from in Software Update Point Component properties. When you select to run the WSUS cleanup task, it will run at the next software updates synchronization. The expired software updates will be set to a status of declined on the WSUS server and the Windows Update Agent on computers will no longer scan these software updates. By default, the WSUS cleanup job runs every 30 days.  
  
#### To schedule and run the WSUS cleanup job  
  
1.  In the Configuration Manager console, navigate to **Administration** > **Overview** > **Site Configuration** > **Sites**.  
  
2.  Click **Configure Site Components** in the **Settings** group, and then click **Software Update Point** to open Software Update Point Component Properties.  
  
3.  Click the **Supersedence Rules** tab, select **Run WSUS cleanup wizard**, and then click **OK**.  
  
## See Also  
 [Deploy and manage software updates in System Center Configuration Manager](../Topic/Deploy%20and%20manage%20software%20updates%20in%20System%20Center%20Configuration%20Manager.md)