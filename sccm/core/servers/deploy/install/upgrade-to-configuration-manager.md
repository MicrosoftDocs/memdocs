---
title: "Upgrade to System Center Configuration Manager | Microsoft Docs"
description: "Learn the steps for running a successful in-place upgrade from a site and hierarchy that runs System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Upgrade to System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can run an in-place upgrade to upgrade to System Center Configuration Manager from a site and hierarchy that runs System Center 2012 Configuration Manager.  

 Before upgrading from System Center 2012 Configuration Manager, you must prepare sites which requires you to remove specific configurations that can prevent a successful upgrade, and then follow the upgrade sequence when more than a single site is involved.  

 > [!TIP]
 > When managing System Center Configuration Manager site and hierarchy infrastructure, the terms *upgrade*, *update*, and *install* are used to describe three separate concepts.. To learn how each term is used, see [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install).

##  <a name="bkmk_path"></a> In-place upgrade paths  

**Upgrade to version 1702**   
When you have version 1702 baseline media, you can upgrade the following to a fully licensed version of System Center Configuration Manager version 1702:   
-	  An evaluation install of System Center Configuration Manager version 1702
-	  System Center 2012 Configuration Manager with Service Pack 1
-	  System Center 2012 Configuration Manager with Service Pack 2
-	  System Center 2012 R2 Configuration Manager
-	  System Center 2012 R2 Configuration Manager with Service Pack 1

**Upgrade to version 1606**  
On December 15th, 2016, the baseline media for version 1606 was rereleased to add support for additional upgrade scenarios. This new release supports the upgrade of the following to a fully licensed version of System Center Configuration Manager version 1606:  
-   An evaluation install of System Center Configuration Manager version 1606
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  

If you use version 1606 baseline media downloaded prior to December 15th, 2016, you can  upgrade only the following to a fully licensed version of System Center Configuration Manager version 1606:
-   An evaluation install of System Center Configuration Manager version 1606
-   System Center 2012 Configuration Manager with Service Pack 2
-   System Center 2012 R2 Configuration Manager with Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  When you upgrade from a System Center 2012 Configuration Manager version to Current Branch, you might be able to streamline your upgrade process. For more information, see the following:  
>   
>  -   The [Baseline and update versions](../../../../core/servers/manage/updates.md#bkmk_Baselines) section in [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [The CD.Latest folder for System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **The following is not supported:**  
-   It is not supported to upgrade a Technical Preview for System Center Configuration Manager to a fully licensed installation.  A Technical Preview version can  only upgrade to a later version of the Technical Preview.  

-   Migration from a Technical Preview to a fully licensed  version is not supported.  

##  <a name="bkmk_checklist"></a> Upgrade checklists  
 The following check lists can help you plan a successful upgrade to  System Center Configuration Manager.  

### Before you upgrade  

**Review your System Center 2012 Configuration Manager environment** and resolve issues as detailed in the KB4018655: [Configuration Manager clients reinstall every five hours because of a recurring retry task and may cause an inadvertent client upgrade](https://support.microsoft.com/help/4018655).

**Ensure that your computing environment meets the supported configurations** that are required for upgrading to System Center Configuration Manager:  

Review the server operating systems in use to host site system roles:  

-   Some older operating systems supported by System Center 2012 Configuration Manager are not supported by System Center Configuration Manager, and site system roles on those operating systems must be relocated or removed before the upgrade. Review the [Supported Operating Systems for Site System Servers](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md) documentation.   
-   Prerequisite Checker for Configuration Manager does not verify the prerequisites for site system roles on the site server or on remote site systems  

Review required prerequisites for each computer that hosts a site system role:  

-   For example, to deploy an operating system, System Center Configuration Manager uses the Windows 10 Assessment and Deployment Kit (Windows ADK). Before you run Setup, you must download and install Windows 10 ADK on the site server and on each computer that runs an instance of the SMS Provider.  

For general information about supported platforms and prerequisite configurations, see [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

For information about using the Windows ADK with Configuration Manager, see [Infrastructure requirements for operating system deployment in System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

**Review the site and hierarchy status and verify that there are no unresolved issues:**  
Before you upgrade a site, resolve all operational issues for the site server, the site database server, and site system roles that are installed on remote computers. A site upgrade can fail due to existing operational problems.  

**Install all applicable critical updates for operating systems on computers that host the site, the site database server, and remote site system roles:**  
Before you upgrade a site, install any critical updates for each applicable site system. If an update that you install requires a restart, restart the applicable computers before you start the service pack update.  

For more information, see [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Uninstall the site system roles not supported by System Center Configuration Manager:**  
The following site system roles are no longer used in System Center Configuration Manager and must be uninstalled before you upgrade from System Center 2012 Configuration Manager:  

-   Out of Band Management point  
-   System Health Validator point  

**Disable database replicas for management points at primary sites:**  
Configuration Manager cannot successfully upgrade a primary site that has a database replica for management points enabled. Disable database replication before you:  

-   Create a backup of the site database to test the database upgrade  
-   Upgrade the production site to System Center Configuration Manager  

For more information, see the following:  
-   System Center 2012 Configuration Manager:  [Configure Database Replicas for Management Points](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager: [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**Reconfigure software update points that use NLBs:**  
Configuration Manager cannot upgrade a site that uses a Network Load Balancing (NLB) cluster to host software update points.  

If you use NLB clusters for software update points, use PowerShell to remove the NLB cluster. (Beginning with System Center 2012 Configuration Manager SP1, there was no option in the Configuration Manager console to configure an NLB cluster)  

**Disable all site maintenance tasks at each site for the duration of that site's upgrade:**  
Before you upgrade to System Center Configuration Manager, disable any site maintenance task that might run during the time the upgrade process is active. This includes but is not limited to the following:  

-   Backup Site Server  
-   Delete Aged Client Operations  
-   Delete Aged Discovery Data  

When a site database maintenance task runs during the upgrade process, the site upgrade can fail.  

Before you disable a task, record the schedule of the task so you can restore its configuration after the site upgrade completes.  

For more information about site maintenance tasks, see:  

-   System Center 2012 Configuration Manager:  [Planning for Maintenance Tasks for Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager:  [Reference for maintenance tasks for System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**Run Setup Prerequisite Checker**:  
Before you upgrade a site, you can run the **Prerequisite Checker** independently from Setup to validate that your site meets the prerequisites. Later, when you upgrade the site, Prerequisite Checker runs again.  

If you use the baseline media for version 1606 from the October 2016 release, the independent prerequisite check evaluates the site for upgrade to both the Current Branch and the Long-Term Servicing Branch (LTSB) of System Center Configuration Manage. Because some features are not supported by the LTSB, you might see entries in the *ConfigMgrPrereq.log* that are similar to the following:
 - INFO: The site is a LTSB edition.
 - Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.

If you plan to upgrade to the Current Branch, errors for the LTSB edition can be safely ignored. They only apply if you plan to upgrade to the LTSB.

Later, when you run Configuration Manager Setup to do the upgrade, the prerequisite check will run again and evaluate your site based on the branch of System Center Configuration Manager you choose to install (Current Branch, or LTSB). If you choose to upgrade to the Current Branch, the check for features that are not supported by the LTSB are not run.

For more information, see the [Prerequisite Checker](/sccm/core/servers/deploy/install/prerequisite-checker) and [List of Prerequisite Checks for System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Download prerequisite files and redistributable files for System Center Configuration Manager:**    
Use **Setup Downloader** to download prerequisite redistributable files, language packs, and the latest product updates for System Center Configuration Manager.  

For information, see [Setup Downloader](/sccm/core/servers/deploy/install/setup-downloader).  

**Plan to manage server and client languages**:  
When you upgrade a site, the site upgrade installs only the language pack versions you select during the upgrade.  

-   Setup reviews the current language configuration of your site, and then identifies the language packs that are available in the folder where you store previously downloaded prerequisite files.  
-   You can then affirm the selection of the current server and client language packs, or change the selections to add or remove support for languages.  
-   Only language packs that are available when you run Setup (which you get with the prerequisite files that you download) can be selected.  

> [!NOTE]  
>  You cannot use the language packs from System Center 2012 Configuration Manager to enable languages for a System Center Configuration Manager site.  

For more information about language packs, see  [Language Packs in System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Review considerations for site upgrades**:  
When you upgrade a site, some features and configurations reset to a default configuration. To help you prepare for these and related changes, review the information in  [Considerations for upgrading](#bkmk_considerations).  

**Create a backup of the site database at the central administration site and primary sites:**  
Before you upgrade a site, back up the site database to ensure that you have a successful backup to use for disaster recovery.  

See [Backup and recovery for System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Backup a customized Configuration.mof file**:  
If you use a customized Configuration.mof file to define data classes you use with hardware inventory, create a backup of this file before upgrading the site. Then after the upgrade, restore this file to your  site. For more information  about using this file see [How to extend hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Test the database upgrade process on a copy of the most recent site database backup:**  
Before you upgrade a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

-   You should test the site database upgrade process because when you upgrade a site, the site database might be modified  
-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected  
-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality  
-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site  
-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database  

Configuration Manager does not support  the backup of secondary sites nor the test upgrade of a secondary site database.  

It is not supported to run a test database upgrade on the production site database. Doing so upgrades the site database and could render your site inoperable.  

For more information, see [Test the site database upgrade](#bkmk_test).  

**Restart the site server and each computer that hosts a site system role**:  
This is done to ensure that there are no pending actions from a recent installation of updates or from prerequisites, and is an internal process that is company-specific.  

**Upgrade sites**:  
Starting at the top-level site in the hierarchy, run Setup.exe from the System Center Configuration Manager source media.  

After the top-level site upgrades,    you can begin the upgrade of each child site. Complete the upgrade of each site before you begin to upgrade the next site  

Until all sites in your hierarchy upgrade to System Center Configuration Manager, your hierarchy operates in a mixed version mode.  

For information about how to run upgrade, see [Upgrade sites](#bkmk_upgrade).  

### After you upgrade  
**Upgrade stand-alone Configuration Manager consoles**:  
By default, when you upgrade a central administration site or primary site, the installation also upgrades the Configuration Manager console that is installed on the site server. However, you must manually upgrade each console that is installed on a computer other than the site server.  

> [!TIP]  
>  Close each open console before you start the upgrade.  

For more information, see [Install System Center Configuration Manager consoles](../../../../core/servers/deploy/install/install-consoles.md).  

**Reconfigure database replicas for management points at primary sites:**  
If you use database replicas for management points at primary sites, you must uninstall the database replicas before you upgrade the site. After you upgrade a primary site, reconfigure the database replica for management points.   
For more information, see  [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure any database maintenance tasks you disabled prior to the upgrade:**  
If you disabled database [Reference for maintenance tasks for System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) at a site prior to the upgrade, reconfigure those tasks at the site using the same settings that were in place prior to the upgrade.  

**Upgrade clients**:  
After all your sites upgrade to System Center Configuration Manager, plan to upgrade clients.  

When you upgrade a client, the current client software is uninstalled and the new client software version is installed. To upgrade clients, you can use any method that Configuration Manager supports.  

> [!TIP]  
>  When you upgrade the top-level site of a hierarchy, the client installation package on each distribution point in the hierarchy is also updated. When you upgrade a primary site, the client upgrade package that is available from that primary site is updated.  

For information about how to upgrade existing clients and how to install new clients, see [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Considerations for upgrading  
**Automatic actions**:  
When you upgrade to System Center Configuration Manager, the following actions occur automatically:  

-   The site performs a site reset, which includes a reinstallation of all site system roles.  
-   If the site is the top-level site of a hierarchy, it updates the client installation package on each distribution point in the hierarchy. The site also updates the default boot images to use the new Windows PE version that is included with the Windows Assessment and Deployment Kit 10. However, the upgrade does not upgrade existing media for use with image deployment.  
-   If the site is a primary site, it updates the client upgrade package for that site.  

**Manual actions for the administrative user after an upgrade**   
After you upgrade a site, ensure that the following actions are performed:  

-   Ensure that clients that are assigned to each primary site upgrade and install the client software for the new version  
-   Upgrade each Configuration Manager console that connects to the site and that runs on a computer that is remote from the site server  
-   At primary sites where you use database replicas for management points, reconfigure the database replicas  
-   After the site upgrades, you must manually upgrade physical media like ISO files for CDs and DVDs or USB flash drives, or prestaged media used for Windows To Go deployments or provided to hardware vendors. Although the site upgrade updates the default boot images it cannot upgrade these media files or devices used external to Configuration Manager  
-   Plan to update non-default boot images when you do not require the original (older) version of Windows PE.  

**Actions that affect configurations and settings**   
When a site upgrades to System Center Configuration Manager, some configurations and settings do not persist after the upgrade or are set to a new default configuration. The following table are settings that do not persist or that change, and provides details to help you plan for them during a site upgrade:  

-   **Software Center:**  
    The following Software Center items are reset to their default values:  
    -   **Work information** is reset to business hours from **5.00am** to **10.00pm** Monday to Friday.  
    -   The value for **Computer maintenance** is set to **Suspend Software Center activities when my computer is in presentation mode**.  
    -   The value for **Remote control** is set to the value in the client settings that are assigned to the computer.  
-   **Software update summarization schedules:**  
     Custom summarization schedules for software updates or software update groups are reset to the default value of 1 hour. After the upgrade finishes, reset custom summarization values to the required frequency.  

##  <a name="bkmk_test"></a> Test the site database upgrade  
The following information applies only when you are upgrading a prior versoin like System Center 2012 Configuration Manager to System Center Configuration Manager. If your site already runs System Center Configuration Manager and you are installing a new update, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.

Before you upgrade a site, test a copy of that site's database for the upgrade.  

To test the database for an upgrade, you first restore a copy of the site database to an instance of SQL Server that does not host a Configuration Manager site. The version of SQL Server that you use to host the database copy must be a version of SQL Server that the version of Configuration Manager supports that is the source of the database copy.  

Next, after you restore the site database, on the SQL Server computer, run Configuration Manager Setup from the source media folder for System Center Configuration Manager with the **/TESTDBUPGRADE** command-line option.  

-   For information about how to create and restore a backup of a site database, see [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   For information about the **/TESTDBUPGRADE** command-line option, see the table in [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   For information about the supported versions of SQL Server, see the [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) topic.  

> [!TIP]  
>  If you integrate Microsoft Intune with Configuration Manager:  
>   
>  When you run a test database upgrade on copy of the site database that is 5 or more days old, you might receive one of the following messages:  
>   
>  -   WARN: Upgrade will force full sync to cloud.  
>  -   ERROR: Database upgrade will force full sync to cloud.  
>   
> Both can be safely ignored during the testing of a database upgrade as they do not indicate a failure or problem with the test upgrade. Instead, they indicate that during the actual upgrade, data from the **Cloud** database replication group might synchronize with Microsoft Intune.  

Use the following procedure on each central administration site and primary site that you plan to upgrade.  

#### To test a site database for upgrade  

1.  Make a copy of the site database, and then restore that copy to an instance of SQL Server that uses the same edition as your site database and that does not host a Configuration Manager site. For example, if the site database runs on an instance of the Enterprise edition of SQL Server, make sure you restore the database to an instance of SQL Server that also runs the Enterprise edition of SQL Server.  

2.  After you restore the database copy, run Setup from the source media for System Center Configuration Manager. When you run Setup, use the **/TESTDBUPGRADE** command-line option. If the SQL Server instance that hosts the database copy is not the default instance, you must also provide the command-line arguments to identify the instance that hosts the site database copy.  

     For example, you plan to upgrade a site database with the database name SMS_ABC. You restore a copy of this site database to a supported instance of SQL Server with the instance name DBTest. To test an upgrade of this copy of the site database, use the following command line: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     You can find Setup.exe in the following location on the source media for System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

3.  On the instance of SQL Server where you run the database upgrade test, monitor the ConfigMgrSetup.log in the root of the system drive for progress and success:  

    -   If the test upgrade fails, resolve any issues related to the site database upgrade failure, create a new backup of the site database, and then test the upgrade of the new copy of the site database.  
    -   After the process is successful, you can delete the database copy.  

        > [!NOTE]  
        >  It is not supported to restore the copy of the site database that you use for the test upgrade for use as a site database at any site.  

After you successfully upgrade a copy of the site database, proceed with the upgrade of the Configuration Manager site and its site database.  

##  <a name="bkmk_upgrade"></a> Upgrade sites  
After you complete pre-upgrade configurations for your site, test the upgrade of the site database on a database copy, and download prerequisite files and language packs for the service pack version that you plan to install, you are ready to upgrade your Configuration Manager site.  

When you upgrade a site in a hierarchy, you upgrade the top-level site of the hierarchy first. This top-level site is either a central administration site or a stand-alone primary site. After the upgrade of a central administration site is completed, you can upgrade child primary sites in any order that you want. After you upgrade a primary site, you can upgrade that site's child secondary sites, or upgrade additional primary sites before you upgrade any secondary sites.  

To upgrade a central administration site or primary site, you run Setup from the System Center Configuration Manager source media. However, you do not run Setup to upgrade secondary sites. Instead, you use the Configuration Manager console to upgrade a secondary site after you complete the upgrade of its primary parent site.  

Before you upgrade a site, close the Configuration Manager console that is installed on the site server until after the site upgrade is completed. Also, close each Configuration Manager console that runs on computers other than the site server. You can reconnect the console after the site upgrade is completed. However, until you upgrade a Configuration Manager console to the new version of Configuration Manager, that console cannot display some objects and information that are available in new version of Configuration Manager.  

Use the following procedures to upgrade Configuration Manager sites:  

#### To upgrade a central administration site or primary site  

1.  Verify that the user who runs Setup has the following security rights:  

    -   Local Administrator rights on the site server computer.  
    -   Local Administrator rights on the remote site database server for the site, if it is remote.    </br></br>

2.  On the site server computer, open Windows Explorer and browse to **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**.  

3.  Double-click **Setup.exe**. The Configuration Manager Setup wizard opens.  

4.  On the **Before You Begin** page, click **Next**.  

5.  On the **Getting Started** page, select **Upgrade this Configuration Manager site**, and then click **Next**.  

6.  On the **Product Key** page, click **Next**.  

     If you previously installed Configuration Manager Evaluation, you can select **Install the licensed edition of this product**, and then enter your product key for the full installation of Configuration Manager to convert the site to the full version.  

     Beginning with the October 2016 release of the version 1606 baseline media for System Center Configuration Manager, you can specify the expiration date of your Software Assurance agreement. You also have the option to specify the **Software Assurance expiration date** of your licensing agreement as a convenient reminder to you of that date. If you do not enter this during setup, you can specify it later from within the Configuration Manager console.

     >  [!NOTE]   
     >  Microsoft does not validate the expiration date you entered and will not use this date for license validation.  Instead, you can use it as a reminder of your expiration date. This is useful because Configuration Manager periodically checks for new software updates offered  online and your software assurance license status should be current to be eligible to use these additional updates.    

     For more information, see [Licensing and branches for System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

7.  On the **Microsoft Software License Terms** page, read and accept the license terms, and then click **Next**.  

8.  On the **Prerequisite Licenses** page, read and accept the license terms for the prerequisite software, and then click **Next**. Setup downloads and automatically installs the software on site systems or clients when it is required. You must select all check boxes before you can continue to the next page.  

9. On the **Prerequisite Downloads** page, specify whether Setup downloads the latest prerequisite redistributable files, language packs, and the latest product updates from the Internet or use previously downloaded files, and then click **Next**. If you previously downloaded the files by using Setup Downloader, select **Use previously downloaded files** and specify the download folder. For more information, see [Setup Downloader](/sccm/core/servers/deploy/install/setup-downloader).

    > [!NOTE]  
    >  When you use previously downloaded files, verify that the path to the download folder contains the most recent version of the files.  

10. On the **Server Language Selection** page, view the list of languages that are currently installed for the site. Select additional languages that are available at this site for the Configuration Manager console and for reports, or clear languages that you no longer want to support at this site, and then click **Next**. By default, English is selected and cannot be removed.  

    > [!IMPORTANT]  
    >  Each version of Configuration Manager cannot use language packs from a prior version of Configuration Manager. To enable support for a language at a Configuration Manager site that you upgrade, you must use the version of the language pack for that new version. For example, during upgrade from System Center 2012 Configuration Manager to System Center Configuration Manager, if the System Center Configuration Manager version of a language pack is not available with the prerequisite files you download, support for that language cannot be installed.  

11. On the **Client Language Selection** page, view the list of languages that are currently installed for the site. Select additional languages that are available at this site for client computers, or clear languages that you no longer want to support at this site. Specify whether to enable all client languages for mobile device clients, and then click **Next**. By default, English is selected and cannot be removed.  

    > [!IMPORTANT]  
    >  Each version of Configuration Manager cannot use language packs from a prior version of Configuration Manager. To enable support for a language at a Configuration Manager site that you upgrade, you must use the version of the language pack for that new version. For example, during upgrade from System Center 2012 Configuration Manager to System Center Configuration Manager, if the System Center Configuration Manager version of a language pack is not available with the prerequisite files you download, support for that language cannot be installed.  

12. On the **Settings Summary** page, click **Next** to start Prerequisite Checker to verify server readiness for the upgrade of the site.  

13. On the **Prerequisite Installation Check** page, if there are no problems listed, click **Next** to upgrade the site and site system roles. When Prerequisite Checker finds a problem, click an item on the list for details about how to resolve the problem. Resolve all items in the list that have an **Error** status before you continue Setup. After you resolve the issue, click **Run Check** to restart prerequisite checking. You can also open the ConfigMgrPrereq.log file in the root of the system drive to review the Prerequisite Checker results. The log file can contain additional information that is not displayed in the user interface. For a list of installation prerequisite rules and descriptions, see [Prerequisite Checker](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

On the **Upgrade** page, Setup displays the overall progress status. When Setup completes the core site server and site system installation, you can close the wizard. Site configuration continues in the background.  

#### To upgrade a secondary site  

1.  Verify that the administrative user that runs Setup has the following security rights:  

    -   Local Administrator rights on the secondary site computer  
    -   Infrastructure Administrator or a Full Administrator security role on the parent primary site  
    -   System administrator (SA) rights on the site database of the secondary site  
    </br>
2.  In the Configuration Manager console, click **Administration**.  

3.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

4.  Select the secondary site that you want to upgrade, and then, on the **Home** tab, in the **Site** group, click **Upgrade**.  

5.  Click **Yes** to confirm the decision, and to start the upgrade of the secondary site.  

The secondary site upgrade progresses in the background. After the upgrade is completed, you can confirm the status in the Configuration Manager console. To confirm the status, select the secondary site server, and then on the **Home** tab, in the **Site** group, click **Show Install Status**.  

##  <a name="BKMK_PostUpgrade"></a> Perform post-upgrade tasks  
After you upgrade a site to a new service pack, you might have to complete additional tasks to finish the upgrade or reconfigure the site. These tasks can include the upgrade of Configuration Manager clients or Configuration Manager consoles, re-enabling database replicas for management points, or restoring settings for Configuration Manager functionality that you use and that does not persist after the service pack upgrade.  

**Known issues for Secondary sites:**  
- **When you upgrade to version 1511:** To ensure clients at secondary sites can find the management point from the secondary site (proxy management point), manually add the management point to boundary groups that also include the distribution points at the secondary site.  

- **When you upgrade to version 1606 or later:** Proxy management points are automatically added to boundary groups that include distribution points at the secondary site.
