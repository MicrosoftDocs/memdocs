---
title: "In-console updates | Microsoft Docs"
description: "System Center Configuration Manager synchronizes with the Microsoft cloud to get updates you can install within the console."
ms.custom: na
ms.date: 4/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brendunsms.author: brendunsmanager: angrobe

---
# Install in-console updates for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
System Center Configuration Manager synchronizes with the Microsoft cloud service to get updates. You can then install these updates from within the Configuration Manager console.

## Get available updates
Only updates that apply to your infrastructure and version are downloaded and made available to your hierarchy. This synchronization can be automatic or manual, depending on how you configure the service connection point for your hierarchy:

-   In **online mode**, the service connection point automatically connects to the Microsoft cloud service and downloads applicable updates.  

     By default, Configuration Manager checks for new updates every 24 hours. You can also check for updates immediately by choosing **Check for Updates** in the **Administration** > **Updates and Servicing** node of the Configuration Manager console. (Prior to version 1702, this node was under **Administration** > **Cloud Services**.)

-   In **offline mode**, the service connection point does not connect to the Microsoft cloud service. You must manually [use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) to download and then import available updates.  

> [!NOTE]  
>  In addition to the updates that you get when synchronizing with the Microsoft cloud service, out-of-band fixes that are installed by using the [Update Registration Tool](http://technet.microsoft.com/library/mt691544.aspx) are also imported into your console where you can then select them to install.  

After updates are synchronized you can view them in the Configuration Manager console by going to the **Administration** > **Updates and Servicing** node:  

-   Updates you have not installed display as **Available**.

-   Updates you have installed display as **Installed**.  Only the most recently installed update is shown. You can choose the **History** button on the ribbon to view previously installed updates.



Before you configure the service connection point, understand and plan for its additional uses. The following uses might affect how you configure this site system role:  

-   The service connection point is used to upload usage information about your site. This information helps the Microsoft cloud service identify the updates that are available for the current version of your infrastructure. For more information, see [Diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   The service connection point is used to manage devices with Microsoft Intune, and using Configuration Manager on-premises mobile device management. For more information, see   [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

To better understand what happens when updates are downloaded, see:  

-   [Flowchart - Download updates for System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Flowchart - Update replication for System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## Assign permissions to view and manage updates and features
To view updates in the console, a user must be assigned a role-based administration security role that includes the security class named **Update packages**. This class grants access to view and manage updates in the Configuration Manager console.    

**About the Update packages class:**  
By default, **Update packages** (SMS_CM_Updatepackages) is part of the following built-in security roles with the listed permissions:
 -  **Full Administrator** with **Modify** and **Read** permissions:
    -   A user with this security role and access to the **All** security scope can view updates, install updates and enable features during the installation, and enable individual features after the update is installed.
    - A user with this security role and access to the **Default** security scope can view updates, install updates and enable features during the installation, and view features after an update is installed. But this user cannot enable the features after the update is installed.

- **Read-only Analyst** with **Read** permissions:
  -  A user with this security role and access to the **Default** scope can view updates but not install them. This user can also view features after an update has installed but cannot enable them.

**Permissions required for updates and servicing:**   
  - Use an account that is assigned a security role that includes the **Update packages** class with both **Modify** and **Read** permissions.
  - The account must be assigned the **Default** scope.

**Permissoins to only view updates**:
  - Use an account that is assigned a security role that includes **Update packages** class with only the **Read** permission.
  - The account must be assigned the **Default** scope.

**Permissions required to enable features after updates are installed:**
  -  Use an account that is assigned a security role that includes the **Update packages** class with both **Modify** and **Read** permissions.
  -  The account must be assigned the **All** scope.






##  <a name="bkmk_beforeinstall"></a> Before you install an in-console update  
 Review the following steps before you install an update from within the Configuration Manager console.  

###  <a name="bkmk_step1"></a> Step 1: Review the update checklist  
Review the applicable update checklist for actions to take before you start the update:

- Update to 1606: See [Checklist for installing update 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Update to 1610 from either 1606: See [Checklist for installing update 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Update to 1702 from either 1606 or 1610: See [Checklist for installing update 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

###  <a name="bkmk_step2"></a> Step 2: Test the database upgrade before installing an update  
The information in this step applies only when you are installing an *update* for a System Center Configuration Manager site. If you are *upgrading* a System Center 2012 Configuration Manager site to System Center Configuration Manager, see [Test the site database upgrade](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Before you install a new update in your hierarchy, like update 1610, you can test the upgrade of your site database. The name of the command-line option that you use to test installing an update to a backup of your site database is **testdbupgrade**.  

If installing an update fails, you should not need to perform a site recovery. Instead, you can retry the update installation. So, although the test upgrade of the database is less critical than it was in past product versions like System Center 2012 Configuration Manager, we still recommend it.


#### To run testdbupgrade before installing an update  

1.  Get a set of source files from the **CD.Latest** folder of a site that runs the version that you plan to update to. This might require you to first install a site in a lab or test environment that runs that version of System Center Configuration Manager.  

     The **CD.Latest** folder for a site has the source files for that version. You must use these source files to run the test upgrade of your site database. For more information, see [The CD.Latest folder for System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

     For example, if your site runs version 1606 and you want to update to 1610, you must get a CD.Latest folder from a site that has already updated to version 1610. Typically, you can install a new and temporary site in a lab, and upgrade that to version 1610 to create the CD.Latest folder with the required files.  

2.  Copy the CD.Latest folder to a location on the SQL Server instance that you will use to run the test database upgrade.

3.  Create a backup of the site database that you want to test upgrade, and then restore a copy of that database to an instance of SQL Server that does not host a Configuration Manager site. The SQL Server instnace must use the same edition of SQL Server as your site database.  

4.  After you restore the database copy, run **Setup** from the CD.Latest folder that you copied from your lab or test environment. When you run Setup, use the **/TESTDBUPGRADE** command-line option. If the SQL Server instance that hosts the database copy is not the default instance, you must also provide the command-line arguments to identify the instance that hosts the site database copy.  

     For example, assume you plan to upgrade a site database with the database name SMS_ABC. You restore a copy of this site database to a supported instance of SQL Server with the instance name DBTest. To test an upgrade of this copy of the site database, use the following command line: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     You can find Setup.exe in the following location on the source media for System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  On the instance of SQL Server where you run the database upgrade test, monitor the ConfigMgrSetup.log in the root of the system drive for progress and success.  

     If the test upgrade fails, fix any issues related to the site database upgrade failure, create a new backup of the site database, and then test the upgrade of the new copy of the site database.  

     After the process is successful, you can delete the database copy.  

    > [!NOTE]  
    >  It is not supported to restore the copy of the site database that you use for the test upgrade for use as a site database at any site.  

###  <a name="bkmk_step3"></a> Step 3: Run the prerequisite checker before installing an update  
Before you install an update, consider running the prerequisite check for that update. If you run the prerequisite before installing an update:  

-   The update files are replicated to other sites in advance of installing the update.  

-   The prerequisite check will automatically run again when you choose to install the update.  

Later, when you install the update, you have the option to configure the update to ignore prerequisite check warnings.  

#### To run the prerequisite checker before installing an update  

1.  In the Configuration Manager console, go to **Administration** > **Updates and Servicing**.   

2.  Right click on the update package you want to run the prerequisite check for.  

3.  Choose **Run prerequisite check**.  

     When you run the prerequisite check, content for the update replicates to child sites.  You can view the distmgr.log on the site server to confirm that content replicates successfully.  

4.  To view the results of the check, in the Configuration Manager console go to **Monitoring** > **Updates and Servicing Status** and look for the prerequisite status. You can also view the ConfigMgrPrereq.log on the site server for more details.  



##  <a name="bkmk_install"></a> Install in-console updates  
 When you are ready to install updates from within the Configuration Manager console, you begin with the top-tier site of your hierarchy. This is either the central administration site or a stand-alone primary site.  

 We recommend that you plan to install the update outside normal business hours for each site. The process of installing the update and its actions to reinstall site components and site system roles will then have the least effect on your business operations.  

-   Child primary sites start the update automatically after the central administration site completes installation of the update. This is the default and recommended process. However, you can use [Service windows for site servers](/sccm/core/servers/manage/service-windows) to control when a primary site installs updates.  

-   You must manually update secondary sites from within the Configuration Manager console after the primary parent site update is complete. Automatic update of secondary site servers is not supported.  

-   When you use a Configuration Manager console after the site is updated, you are prompted to update the console.  

-  After the site server successfully completes installation of an update, it automatically updates all applicable site system roles.  The only caveat to this is for distribution points. When installing an update, all distribution points do not reinstall and go offline to update at the same time. Instead, the site server uses the site's content distribution settings to distribute the update to a subset of distribution points at a time. The result is that only some distribution points go off-line to install the update. This allows distribution points that have not yet begun to update or that have completed the update to remain on-line and able to provide content to clients.


###  <a name="bkmk_overview"></a> Overview of in-console update installation  
**1. When the update installation starts**  
You are presented with the Updates Wizard that displays a list of the product areas that the update applies to.  

-   On the **General** page of the wizard, you can configure **Prerequisite warnings**.  
      -   Prerequisite errors always stop the update installation. You must fix errors before you can successfully retry the update installation. See [Retry installation of a failed update](#bkmk_retry) for more information.  

    -   Prerequisite warnings can also stop the update installation. You should fix warnings before you retry the update installation. See [Retry installation of a failed update](#bkmk_retry) for more information.  
    -   Selecting the option **Ignore any prerequisite check warnings and install this update regardless of missing requirements**, sets a condition for the update installation that ignores prerequisite warnings. This allows the update installation to continue. If you do not select this option, the update installation will stop when a warning is encountered. Unless you have previously run the prerequisite check and fixed prerequisite warnings for a site, we do not recommend use of this option.  

      In both the **Administration** and **Monitoring** workspaces, the Updates and Servicing node includes a button on the Ribbon named **Ignore prerequisite warnings**. This button becomes available when an update package fails to complete installation due to prerequisite check warnings. For example, if you install an update without using the option to ignore prerequisite warnings (from within the Updates Wizard), and that update installation stops with a state of prerequisite warning but no errors, you can later choose **Ignore prerequisite warnings** from the ribbon to trigger an automatic continuation of that update installation that then ignores prerequisite warnings. When you use this option, the update installation automatically continues after a few minutes.



-   When an update applies to the Configuration Manager client, you are presented with the option to test the client update with a limited set of clients. For more information, see [How to test client upgrades in a pre-production collection in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. During the update installation**  
As part of the update installation, Configuration Manager:  

-   Reinstalls any affected components, like site system roles or the Configuration Manager console.  

-   Manages updates to clients based on the selections that you made for client piloting, and for [automatic client upgrades](https://technet.microsoft.com/library/mt627885.aspx).  

-   Will not need to restart site system servers as part of the update (unless .NET is installed as part of a site system roles prerequisite).  

> [!TIP]  
>  When updates are installed,  Configuration Manager also updates the CD.Latest folder. This folder is used during a site recovery.  

**3. Monitor the progress of updates as they install**  
Use the following to monitor progress:  

-   In the Configuration Manager console: **Administration** > **Updates and Servicing** node. This node shows the installation status for all update packages.


-   In the Configuration Manager console: **Monitoring** > **Overview** > **Updates and Servicing Status** node. This node shows the installation status of only the update package that is currently being installed.  

  The update pack installation is broken down to the following phases for ease of monitoring. For each phase, additional details include which log file to view for more information.:  
    -   **Download** (This phase applies only to the top-tier site where the service connection point site system role is installed.)
    -   **Replication**
    -   **Prerequisites Check**
    -   **Installation**
    -   **Post Installation** (This phase is available beginning with version 1610.)

-   You can view the **CMUpdate.log** file in **&lt;ConfigMgr_Installation_Directory>\Logs**  

**4. When the update installation completes**  
After the first site update completes installation:  

-   Child primary sites will install the update automatically. No further action is required.  

-   Secondary sites must be manually updated from within the Configuration Manager console.
> [!TIP]
> Although the version of a secondary site does not display in the console, you can use the Configuration Manager SDK to confirm a site's version. See [SMS_Site Server WMI Class](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Until all sites in your hierarchy update to the new version, your hierarchy operates in a mixed version mode. For more information, see [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Update Configuration Manager consoles**  
After a central administration site or primary site updates, each Configuration Manager console that connects to that site must also update. You are prompted to update a console:  

-   When you open the console.  

-   When you go to a new node in an open console.  

We recommend that you install the update immediately.  

After the console update completes, you can verify the console and site version is correct. Go to **About System Center Configuration Manager** at the top-left corner of the console.  

###  <a name="bkmk_toptier"></a> To start the update installation at the top-tier site  
At the top-tier site of your hierarchy, in the Configuration Manager console go to **Administration** > **Updates and Servicing**, select an **Available** update, and then click **Install Update Pack**.  

###  <a name="bkmk_secondary"></a> To start the update installation at a secondary site  
After a secondary sites parent primary site is updated, you can then update the secondary site from within the Configuration Manager console.  To do so, you use the **Upgrade Secondary Site Wizard**.  

1.  In the Configuration Manager console go to **Administration** > **Site Configuration** > **Sites**, select the site you want to update, and then on the Home tab, in the **Site** group, choose **Upgrade**.  

2.  Click **Yes** to start the update of the secondary site.  

To monitor the update installation on a secondary site, select the secondary site server. Then on the **Home** tab, in the **Site** group, choose **Show Install Status**. You can also add the **Version** column to the console display so that you can view the version of each secondary site.  

After a secondary site is successfully updated, if the status in the console does not refresh or suggests the update has failed, you can use the **Retry installation** option. This option does not reinstall the update for a secondary site that did successfully install the update, but will force the console to update the status.


##  <a name="bkmk_retry"></a> Retry installation of a failed update  
When an update fails to be installed, review the in-console feedback to identify resolutions for warnings and errors. You can also view the ConfigMgrPrereq.log on the site server for more details. Before you retry the installation of an update, you must fix errors, and should fix warnings.  

When you are ready to retry the installation of an update, select the failed update and then choose an applicable option. The update installation retry behavior depends on the node where you start the retry, and the retry option that you use.  

1.  **Retry installation for the hierarchy:**  
You can retry the installation of an update for the entire hierarchy when that update is in one of the following states:  

    -   Prerequisite check passed with one or more warnings, and the option to ignore prerequisite check warnings was not set in the Update Wizard. (The update's value for **Ignore Prereq Warning** in the **Updates and servicing** node is **No**.)   
    -   Prerequisite failed    
    -   Installation failed
    -   Replication of the content to the site failed   

    Go to **Administration** > **Updates and Servicing**, select the update, and then choose one of the following:  

    -   **Retry** - When you run **Retry** from this node, the update install starts again and will automatically ignore prerequisite warnings. It will also re-replicate content for the update if replication previously failed.
    - **Ignore prerequisite warnings** - Beginning with version 1606, if the update install stops due to a warning, you can then choose **Ignore prerequisite warnings**. This action allows the installation of the update to continue (after a few minutes) and uses the option to ignore prerequisite warnings.   

2.  **Retry installation for the site:**  
 You can retry the installation of an update at a specific site when that update is in one of the following states:  

    -   Prerequisite check passed with one or more warnings, and option to ignore prerequisite check warnings was not set in the Update Wizard (The updates value for **Ignore Prereq Warning** in the Updates and servicing node is **No**.)  
    -   Prerequisite failed    
    -   Installation failed    

    Go to **Monitoring** > **Overview** > **Site Servicing Status**, select the update and then click one of the following:

       - **Retry** - When you run **Retry** from this node, you restart the installation of the update at only that site. Unlike running **Retry** from the **Updates and Servicing** node, this retry does not ignore prerequisite warnings.
       -    **Ignore prerequisite warnings** - Beginning with version 1606, if the update install stops due to a warning, you can then click **Ignore prerequisite warnings**. This action allows the installation of the update to continue (after a few minutes) and uses the option to ignore prerequisite warnings.

##  <a name="bkmk_after"></a> After a site installs an update  
Use the following checklist to complete common tasks and configurations that are made after a site is updated.   

**Confirm site-to-site replication is active:** In the  Configuration Manager console, go to the following locations to view the status and ensure that replication is active:  

-   **Monitoring** > **Overview** > **Site Hierarchy**  

-   **Monitoring** > **Overview** > **Database Replication**  

For more information, see
[Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) and [About the Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirm that site servers and remote site system servers have restarted (if required):** Review your site infrastructure and ensure that applicable site servers and site system servers (remote from the site server) have restarted successfully.  Typically, this is expected only when Configuration Manager installs .NET as a prerequisite for a site system role.  

 **Update stand-alone Configuration Manager consoles:** Ensure that all remote Configuration Manager consoles are update to the same version. You are prompted to update the console when:  

-   You go to a new node in the console.  

-   You open the console.

**Reconfigure database replicas for management points at primary sites:** If you use database replicas for management points at primary sites, you must uninstall the database replicas before you update the site. After you update a primary site, reconfigure the database replica for management points. For more information, see [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure any database maintenance tasks you disabled before the update:** If you disabled database [maintenance tasks for System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) at a site prior to the update, reconfigure those tasks at the site. Use the same settings that were in place before the update.  

**Upgrade clients:** For information about how to upgrade existing clients and how to install new clients, see [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Additional configurations:** Review the changes that you made before you started the update, and then restore those configurations to your sites and hierarchy.  

##  <a name="bkmk_options"></a> Enable optional features from updates  
When you install an update that includes one or more optional features, you will have the opportunity to enable those features in your hierarchy.  You can do so at the time the update is installed, or you can return to the console later and enable the optional features.

To view available features and their status, in the console navigate to **Administration** > **Updates and Servicing** > **Features**.

When a feature is not optional, it's installed automatically and does not appear in the **Features** node.  


When you enable a new feature or pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate, but it can take up to 30 minutes to complete, depending on the HMAN processing cycle. After the change is processed, you must restart the console before you can view new UI related to that feature.


##  <a name="bkmk_prerelease"></a> Use pre-release features from updates
Pre-release features are features that are included in the Current Branch for early testing in a production environment. These features should not be considered production ready, but can be used in your production environement. To learn more about pre-release features, including how to enable them in your environement, see [Pre-release featuers](/sccm/core/servers/manage/pre-release-features).                |


## Known issues

###  <a name="bkmk_faq"></a> Why don't I see certain updates in my console?  
 If you cannot find a specific update (or any updates) in your console after a successful sync with the Microsoft cloud service, this might be because:  

-   The update requires a configuration that your infrastructure does not use, or your current product version does not fulfill a prerequisite for receiving the update.  

     If you believe that you have the required configurations or you meet other prerequisites for a missing update, confirm that your service connection point is in online mode. Then, use the **Check for Updates** option in the **Updates and Servicing** node to force a check.  If you are in offline mode, you must use the service connection tool to manually sync with the cloud service.  

-   Your account lacks the correct role-based administration permissions to view updates in the Configuration Manager console.

    See [Permissions to manage updates](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) in this topic for information about required permissions to view updates and enable features from within the console.

### Why do I see two updates for version 1610
When viewing updates in the console, you might see two updates to install version 1610. These updates have different dates. This happens when one of the following is true:   
-	You installed an earlier version (like 1606) after version 1610 became available

-	You hierarchy runs version 1511 or 1602 and you have not been able to download version 1606

There are two update releases for version 1610 because this update was re-released after some minor changes to some file binaries were made. These changes do not affect the functionality of Configuration Manager or the update.

When both updates are available in your console, we recommend you install the update with the more recent date. However, because both updates deliver the same functionality, if you already installed one of them you do not need to take further action.
-	If you previously installed the older update, you do not need to install the update with the newer date. However, if you do install the newer update after having installed the first update, the binaries in question will update, but no additional change occurs, and no additional actions on your part are needed.

-	If you previously installed the newest update and then install the update with the older date, no additional action is needed. This is because the newer binaries you already installed will not be overwritten by those same binaries from the original update.
