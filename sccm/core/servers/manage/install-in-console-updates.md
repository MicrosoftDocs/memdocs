---
title: In-console updates
titleSuffix: Configuration Manager
description: Install updates to Configuration Manager from the Microsoft cloud 
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Install in-console updates for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager synchronizes with the Microsoft cloud service to get updates. You can then install these updates from within the Configuration Manager console.

## Get available updates
Only updates that apply to your infrastructure and version are downloaded and made available to your hierarchy. This synchronization can be automatic or manual, depending on how you configure the service connection point for your hierarchy:

-   In **online mode**, the service connection point automatically connects to the Microsoft cloud service and downloads applicable updates.  

     By default, Configuration Manager checks for new updates every 24 hours. You can also check for updates immediately by choosing **Check for Updates** in the **Administration** > **Updates and Servicing** node of the Configuration Manager console. 

-   In **offline mode**, the service connection point does not connect to the Microsoft cloud service. To download and then import available updates, [use the Service Connection Tool](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   You can import out-of-band fixes into your console. To do so, use the [update registration tool](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). These out-of-band fixes supplement the updates you get when you synchronize with the Microsoft cloud service.


After updates synchronize, you can view them in the Configuration Manager console by going to the **Administration** > **Updates and Servicing** node:  

-   Updates you have not installed display as **Available**.

-   Updates you have installed display as **Installed**. Only the most recently installed update is shown. You can choose the **History** button on the ribbon to view previously installed updates.



Before you configure the service connection point, understand and plan for its additional uses. The following uses might affect how you configure this site system role:  

-   The service connection point is used to upload usage information about your site. This information helps the Microsoft cloud service identify the updates that are available for the current version of your infrastructure. For more information, see [Diagnostics and usage data](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   The service connection point is used to manage devices with Microsoft Intune, and using Configuration Manager on-premises mobile device management. For more information, see [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

To better understand what happens when updates are downloaded, see:  

-   [Flowchart - Download updates for System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Flowchart - Update replication for System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  



## Assign permissions to view and manage updates and features
To view updates in the console, a user must have a role-based administration security role that includes the security class **Update packages**. This class grants access to view and manage updates in the Configuration Manager console.    

#### About the Update packages class   
By default, the **Update packages** class (SMS_CM_Updatepackages) is part of the following built-in security roles with the listed permissions:
 -  **Full Administrator** with **Modify** and **Read** permissions:
    -   A user with this security role and access to the **All** security scope can view and install updates. The user can also enable features during the installation, and enable individual features after the update is installed.
    - A user with this security role and access to the **Default** security scope can view and install updates. The user can also enable features during the installation, and view features after an update is installed. But this user cannot enable the features after the update is installed.

- **Read-only Analyst** with **Read** permissions:
  -  A user with this security role and access to the **Default** scope can view updates but not install them. This user can also view features after an update has installed but cannot enable them.

#### Permissions required for updates and servicing   
  - Use an account that is assigned a security role that includes the **Update packages** class with both **Modify** and **Read** permissions.
  - The account must be assigned the **Default** scope.

#### Permissions to only view updates   
  - Use an account that is assigned a security role that includes the **Update packages** class with only the **Read** permission.
  - The account must be assigned the **Default** scope.

#### Permissions required to enable features after updates are installed   
  -  Use an account that is assigned a security role that includes the **Update packages** class with both **Modify** and **Read** permissions.
  -  The account must be assigned the **All** scope.



##  <a name="bkmk_beforeinstall"></a> Before you install an in-console update  
 Review the following steps before you install an update from within the Configuration Manager console.  

###  <a name="bkmk_step1"></a> Step 1: Review the update checklist  
Review the applicable update checklist for actions to take before you start the update:

- [Checklist for installing update 1706](../../../core/servers/manage/checklist-for-installing-update-1706.md)  

- [Checklist for installing update 1710](../../../core/servers/manage/checklist-for-installing-update-1710.md)  

- [Checklist for installing update 1802](../../../core/servers/manage/checklist-for-installing-update-1802.md)


###  Step 2: Run the prerequisite checker before installing an update  
Before you install an update, consider running the prerequisite check for that update. If you run the prerequisite before installing an update:  

-   The update files are replicated to other sites before installing the update.  

-   The prerequisite check automatically runs again when you choose to install the update.  

> [!NOTE]   
> When you start a prerequisite check and then view the status, the **Installation** phase appears to be active, however the update is not actually installing. To run the prerequisite check, the update process extracts the package from the content library and puts it into a staging folder where the current prerequisite checks can be accessed. This same process runs when you install an update. For this reason, Installation shows as ‘In progress’. Only the *Extract Update package* step is shown in the Installation category.  

Later, when you install the update, you can configure the update to ignore prerequisite check warnings.  

#### To run the prerequisite checker before installing an update  

1.  In the Configuration Manager console, go to **Administration** > **Updates and Servicing**.   

2.  Right-click on the update package you want to run the prerequisite check for.  

3.  Choose **Run prerequisite check**.  

     When you run the prerequisite check, content for the update replicates to child sites. You can view the distmgr.log on the site server to confirm that content replicates successfully.  

4.  To view the results of the check, in the Configuration Manager console go to **Monitoring** > **Updates and Servicing Status** and look for the prerequisite status. You can also view the ConfigMgrPrereq.log on the site server for more details.  



##  <a name="bkmk_install"></a> Install in-console updates  
 When you are ready to install updates from within the Configuration Manager console, you begin with the top-tier site of your hierarchy. This site is either the central administration site or a stand-alone primary site.  

 We recommend that you install the update outside normal business hours for each site to minimize the effect on business operations. This recommendation is because the update installation might include actions like reinstalling site components and site system roles.  

-   Child primary sites start the update automatically after the central administration site completes installation of the update. This process is by default and recommended. However, you can use [Service windows for site servers](/sccm/core/servers/manage/service-windows) to control when a primary site installs updates.  

-   Manually update secondary sites from within the Configuration Manager console after the primary parent site update is complete. Automatic update of secondary site servers is not supported.  

-   When you use a Configuration Manager console after the site is updated, you are prompted to update the console.  

-  After the site server successfully completes installation of an update, it automatically updates all applicable site system roles. The only caveat is for distribution points. When installing an update, all distribution points do not reinstall and go offline to update at the same time. Instead, the site server uses the site's content distribution settings to distribute the update to a subset of distribution points at a time. The result is that only some distribution points go off-line to install the update. Distribution points that have not begun to update or that have completed the update remain on-line and able to provide content to clients.


###  <a name="bkmk_overview"></a> Overview of in-console update installation  
#### 1. When the update installation starts  
You are presented with the Updates Wizard that displays a list of the product areas that the update applies to.  

-   On the **General** page of the wizard, you can configure **Prerequisite warnings**.  
    -   Prerequisite errors always stop the update installation. Fix errors before you can successfully retry the update installation. For more information, see [Retry installation of a failed update](#bkmk_retry).  

    -   Prerequisite warnings can also stop the update installation. Fix warnings before you retry the update installation. For more information, see [Retry installation of a failed update](#bkmk_retry).  
    -   **Ignore any prerequisite check warnings and install this update regardless of missing requirements**: sets a condition for the update installation to ignore prerequisite warnings. This option allows the update installation to continue. If you do not select this option, the update installation stops when a warning is encountered. Unless you have previously run the prerequisite check and fixed prerequisite warnings for a site, we do not recommend use of this option.  

      In both the **Administration** and **Monitoring** workspaces, the Updates and Servicing node includes a button on the Ribbon named **Ignore prerequisite warnings**. This button becomes available when an update package fails to complete installation due to prerequisite check warnings. For example, you install an update without using the option to ignore prerequisite warnings (from within the Updates Wizard). The update installation stops with a state of prerequisite warning but no errors. Later you can choose **Ignore prerequisite warnings** from the ribbon to trigger an automatic continuation of that update installation that then ignores prerequisite warnings. When you use this option, the update installation automatically continues after a few minutes.



-   When an update applies to the Configuration Manager client, you are presented with the option to test the client update with a limited set of clients. For more information, see [How to test client upgrades in a pre-production collection](../../../core/clients/manage/upgrade/test-client-upgrades.md).  


#### 2. During the update installation  
As part of the update installation, Configuration Manager:  

-   Reinstalls any affected components, like site system roles or the Configuration Manager console.  

-   Manages updates to clients based on the selections that you made for client piloting, and for [automatic client upgrades](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

-   Doesn't restart site system servers as part of the update unless .NET is installed as part of a site system roles prerequisite.  

> [!TIP]  
>  When updates are installed, Configuration Manager also updates the CD.Latest folder. This folder is used during a site recovery.  


#### 3. Monitor the progress of updates as they install  
Use the following to monitor progress:  

-   In the Configuration Manager console: **Administration** > **Updates and Servicing** node. This node shows the installation status for all update packages.


-   In the Configuration Manager console: **Monitoring** > **Overview** > **Updates and Servicing Status** node. This node shows the installation status of only the update package that is currently being installed.  

    The update pack installation is broken down to the following phases for ease of monitoring. For each phase, additional details include which log file to view for more information:  
    -   **Download** (This phase applies only to the top-tier site where the service connection point site is installed.)   

    -   **Replication**   

    -   **Prerequisites Check**   

    -   **Installation**    

    -   **Post Installation** - For more information, see [post installation tasks](#post-installation-tasks).  

-   You can view the **CMUpdate.log** file in **&lt;ConfigMgr_Installation_Directory>\Logs**  


#### 4. When the update installation completes  
After the first site update completes installation:  

-   Child primary sites install the update automatically. No further action is required.  

-   Secondary sites must be manually updated from within the Configuration Manager console.
> [!TIP]
> Although the version of a secondary site does not display in the console, you can use the Configuration Manager SDK to confirm a site's version. See [SMS_Site Server WMI Class](/sccm/develop/reference/core/servers/configure/sms_site-server-wmi-class).


-   Until all sites in your hierarchy update to the new version, your hierarchy operates in a mixed version mode. For more information, see [Interoperability between different versions of Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


#### 5. Update Configuration Manager consoles  
After a central administration site or primary site updates, each Configuration Manager console that connects to that site must also update. You are prompted to update a console:  

-   When you open the console

-   When you go to a new node in an open console

We recommend that you install the update immediately.  

After the console update completes, you can verify the console and site version is correct. Go to **About System Center Configuration Manager** at the top-left corner of the console.  

 > [!Note]  
 > Starting in version 1802, the console version is now slightly different from the site version. The minor version of the console now corresponds to the Configuration Manager release version. For example, in Configuration Manager version 1802 the initial site version is 5.0.8634.1000, and the initial console version is 5.**1802**.1082.1700. The build (1082) and revision (1700) numbers may change with future hotfixes to the 1802 release.



###  <a name="bkmk_toptier"></a> To start the update installation at the top-tier site  
At the top-tier site of your hierarchy, in the Configuration Manager console go to **Administration** > **Updates and Servicing**, select an **Available** update, and then click **Install Update Pack**.  


###  <a name="bkmk_secondary"></a> To start the update installation at a secondary site  
After a secondary site's parent primary site updates, you can update the secondary site from within the Configuration Manager console. To do so, you use the **Upgrade Secondary Site Wizard**.  

1.  In the Configuration Manager console go to **Administration** > **Site Configuration** > **Sites**, select the site you want to update, and then on the Home tab, in the **Site** group, choose **Upgrade**.  

2.  Click **Yes** to start the update of the secondary site.  

To monitor the update installation on a secondary site, select the secondary site server. Then on the **Home** tab, in the **Site** group, choose **Show Install Status**. You can also add the **Version** column to the console display so that you can view the version of each secondary site.  

After a secondary site successfully updates, if the status in the console does not refresh or suggests the update has failed, use the **Retry installation** option. This option does not reinstall the update for a secondary site that did successfully install the update, but forces the console to update the status.


### Post Installation tasks
When a site installs an update, there are several tasks that cannot start until after the update completes installation on the site server. Following is a list of the post installation tasks that are critical for site and hierarchy operations. Because they are critical, they are actively monitored. Additional tasks that are not directly monitored include the reinstallation of site system roles. To view the status of the critical post installation tasks, select **Post Installation** task while monitoring the update installation for a site.

Not all tasks complete immediately. Some tasks don't start until each site completes installation of the update. New functionality you might expect can be delayed until these tasks complete. Turning on new features doesn't start until all sites complete update installation, so new features might not be visible for some time.

The post installation tasks include:

-   **Installing SMS_EXECUTIVE service**
  -   Critical service that runs on the site server.
  -   Reinstallation of this service should complete quickly.


-   **Installing SMS_DATABASE_NOTIFICATION_MONITOR component**
  -   Critical site component thread of SMS_EXECUTIVE service.
  -   Reinstallation of this service should complete quickly.


-   **Installing SMS_HIERARCHY_MANAGER component**
  -   Critical site component that runs on the site server.
  -   Responsible for reinstalling site system roles on site system servers. Status for individual site system role reinstallation does not display.
  -   Reinstallation of this service should complete quickly.


-   **Installing SMS_REPLICATION_CONFIGURATION_MONITOR component**
  -   Critical site component that runs on the site server.
  -   Reinstallation of this service should complete quickly.


-   **Installing SMS_POLICY_PROVIDER component**
  -   Critical site component that runs only on primary sites.
  -   Reinstallation of this service should complete quickly.


-   **Monitoring replication initialization**   
  -   This task only displays at the central administration site and child primary sites.
  -   Dependent on the SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Should complete quickly.


-   **Updating Configuration Manager Client Preproduction Package**    
  -   This task displays even when client preproduction (also called client piloting) isn't enabled for use.
  -   Doesn't start until all sites in the hierarchy finish installing the update.


-   **Updating Client folder on Site Server**
  -   This task doesn't display if you use the client in preproduction.  
  -   Should complete quickly.


-   **Updating Configuration Manager Client Package**
  -   This task doesn't display if you use the client in preproduction.  
  -   Finishes only after all sites install the update.  


-   **Turning on Features**
  -   This task displays only at the top-tier site of the hierarchy.
  -   Doesn't start until all sites in the hierarchy finish installing the update.
  -   Individual features aren't displayed.



##  <a name="bkmk_retry"></a> Retry installation of a failed update  
When an update fails to install, review the in-console feedback to identify resolutions for warnings and errors. You can also view the ConfigMgrPrereq.log on the site server for more details. Before you retry the installation of an update, you must fix errors, and should fix warnings.  

> [!TIP]  
> If an update has problems downloading or replicating, you can use the [update reset tool](/sccm/core/servers/manage/update-reset-tool). 

When you are ready to retry the installation of an update, select the failed update and then choose an applicable option. The update installation retry behavior depends on the node where you start the retry, and the retry option that you use.  

#### Retry installation for the hierarchy
You can retry the installation of an update for the entire hierarchy when that update is in one of the following states:  

  -   Prerequisite checks passed with one or more warnings, and the option to ignore prerequisite check warnings was not set in the Update Wizard. (The update's value for **Ignore Prereq Warning** in the **Updates and servicing** node is **No**.)   
  -   Prerequisite failed    
  -   Installation failed
  -   Replication of the content to the site failed   

Go to **Administration** > **Updates and Servicing**, select the update, and then choose one of the following options:  

  -   **Retry** - When you run **Retry** from this node, the update install starts again and automatically ignores prerequisite warnings. Content for the update also re-replicates if replication previously failed.
  - **Ignore prerequisite warnings** - If the update install stops due to a warning, you can then choose **Ignore prerequisite warnings**. This action allows the installation of the update to continue (after a few minutes) and uses the option to ignore prerequisite warnings.   

#### Retry installation for the site  
 You can retry the installation of an update at a specific site when that update is in one of the following states:  

  -   Prerequisite checks passed with one or more warnings, and option to ignore prerequisite check warnings was not set in the Update Wizard. (The updates value for **Ignore Prereq Warning** in the Updates and servicing node is **No**.)  
  -   Prerequisite failed    
  -   Installation failed    

Go to **Monitoring** > **Overview** > **Site Servicing Status**, select the update, and then click one of the following options:

  - **Retry** - When you run **Retry** from this node, you restart the installation of the update at only that site. Unlike running **Retry** from the **Updates and Servicing** node, this retry does not ignore prerequisite warnings.
  - **Ignore prerequisite warnings** - If the update install stops due to a warning, you can then click **Ignore prerequisite warnings**. This action allows the installation of the update to continue (after a few minutes) and uses the option to ignore prerequisite warnings.



##  <a name="bkmk_after"></a> After a site installs an update  
Use the following checklist to complete common tasks and configurations that are made after a site is updated.   

**Confirm site-to-site replication is active:** In the  Configuration Manager console, go to the following locations to view the status and ensure that replication is active:  

-   **Monitoring** > **Overview** > **Site Hierarchy**  

-   **Monitoring** > **Overview** > **Database Replication**  

For more information, see
[Monitor hierarchy and replication infrastructure](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) and [About the Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirm that site servers and remote site system servers have restarted (if necessary):** Review your site infrastructure and ensure that applicable site servers and site system servers have restarted successfully. Typically, site servers restart only when Configuration Manager installs .NET as a prerequisite for a site system role.  

 **Update stand-alone Configuration Manager consoles:** Ensure that all remote Configuration Manager consoles are update to the same version. You are prompted to update the console when:  

-   You go to a new node in the console.  

-   You open the console.

**Reconfigure database replicas for management points at primary sites:** If you use database replicas for management points at primary sites, you must uninstall the database replicas before you update the site. After you update a primary site, reconfigure the database replica for management points. For more information, see [Database replicas for management points](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure any database maintenance tasks you disabled before the update:** If you disabled database [maintenance tasks](../../../core/servers/manage/maintenance-tasks.md) at a site before installing the update, reconfigure those tasks at the site. Use the same settings that were in place before the update.  

**Upgrade clients:** For information, see [How to upgrade clients for Windows computers](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Additional configurations:** Review the changes that you made before you started the update, and then restore those configurations to your sites and hierarchy.  



##  <a name="bkmk_options"></a> Enable optional features from updates  
When an update includes one or more optional features, you have the opportunity to enable those features in your hierarchy. You can enable features when the update installs, or you can return to the console later to enable the optional features.

To view available features and their status, in the console navigate to **Administration** > **Updates and Servicing** > **Features**.

When a feature isn't optional, it's installed automatically. It doesn't appear in the **Features** node.  

> [!Important]  
> In a multi-site hierarchy, you can only enable optional or pre-release features from the central administration site. This behavior ensures there are no conflicts across the hierarchy. <!--507197-->
 

When you enable a new feature or pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate, but it can take up to 30 minutes to complete, depending on the HMAN processing cycle. After the change is processed, you must restart the console before you can view new nodes related to that feature.

#### List of optional features
The following features are optional in the latest version of Configuration Manager:<!--505213-->  
- [Conditional access for managed PCs](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->
- [Passport for Work](/sccm/protect/deploy-use/windows-hello-for-business-settings) (also known as *Windows Hello for Business*) <!--1245704-->
- [VPN for Windows 10](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- [Windows Defender Exploit Guard policy](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [Microsoft Operations Management Suite (OMS) Connector](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) <!--1258052-->
- [PFX Create](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [Client Peer Cache](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [Data warehouse service point](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Surface Driver Updates](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [Task Sequence content pre-caching](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Run Task Sequence Step](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [Create and run scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [Device Health Attestation assessment for compliance policies for conditional access](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [Approve application requests for users per device](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  


> [!Tip]  
> For more information on features that require consent to enable, see [pre-release features](/sccm/core/servers/manage/pre-release-features).  
> For more information on features that are only available in the technical preview branch, see [Technical Preview](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_prerelease"></a> Use pre-release features from updates
Pre-release features are included in the current branch for early testing in a production environment. You can use these features in your production environment, but they are not considered production ready. Learn more about [pre-release features](/sccm/core/servers/manage/pre-release-features), including how to enable them in your environment.             



## Frequently asked questions

###  <a name="bkmk_faq"></a> Why don't I see certain updates in my console?  
 If you can't find a specific update in your console after a successful sync with the Microsoft cloud service, this behavior might be due to one of the following reasons:  

-   The update requires a configuration that your infrastructure does not use, or your current product version does not fulfill a prerequisite for receiving the update.  

     If you believe that you have the required configurations and prerequisites for a missing update, confirm that your service connection point is in online mode. Then, use the **Check for Updates** option in the **Updates and Servicing** node to force a check. If you are in offline mode, you must use the service connection tool to manually sync with the cloud service.  

-   Your account lacks the correct role-based administration permissions to view updates in the Configuration Manager console.

    See [Permissions to manage updates](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) in this topic for information about required permissions to view updates and enable features from within the console.

