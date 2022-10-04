---
title: Checklist for 1602
titleSuffix: Configuration Manager
description: Learn about actions to take before updating from Configuration Manager version 1511 to version 1602.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Checklist for installing update 1602 for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before updating from Configuration Manager version 1511 to version 1602, review the following information and checklist for actions to take before starting the update.  

 **About installing update 1602:**  

 Update 1602 can only be installed at the top-level site of your hierarchy. This means you initiate the installation from your central administration site if you have one, or from your stand-alone primary site.  

-   Child primary sites install the update automatically after the central administration site finishes installing the update. You can use maintenance windows to control when a site installs updates. Beginning with the release of the 1602 update, maintenance windows have been renamed *service windows*. For more information, see [Service windows for site servers](service-windows.md).  

-   You must manually update secondary sites from within the Configuration Manager console after the primary parent site finishes installing the update. Automatic updates of secondary site servers are not supported.  

When the site server installs the update, site system roles that are installed on the site server and those that are installed on remote computers automatically get updated. Therefore, before installing the update, make sure each site system server meets any new prerequisites for operations with the new update version.  

The first time you use a Configuration Manager console after the update has finished, you will be prompted to update that console. To do so, you must run Configuration Manager setup on the computer that hosts the console, and choose the option to update the console. We recommend that you do not delay installing the update to the console.  

 **Checklist:**  

 **Ensure that all sites run a supported version of Configuration Manager:**  Each site server in the hierarchy must run Configuration Manager version 1511 before you can start the installation of update 1602.  

 **Review installed Microsoft .NET versions on site system servers:** When a site installs update 1602, Configuration Manager automatically installs .NET Framework 4.5.2 on each computer that hosts one of the following site system roles (if .NET Framework 4.5 or later is not already installed):  

-   Enrollment proxy point  

-   Enrollment point  

-   Management point  

-   Service connection point  

This installation can put the site system server into a reboot pending state, and report errors to the Configuration Manager component status viewer. Additionally, .NET applications on the server might experience random failures until the server is rebooted.  

 For more information, see [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Review the site and hierarchy status and verify that there are no unresolved issues:** Before you update a site, resolve all operational issues for the site server, the site database server, and site system roles that are installed on remote computers. A site update can fail due to existing operational problems.  

For more information, see [Use the status system](use-status-system.md).  

 **Review file and data replication between sites:**  Ensure that file and database replication between sites is operational and current. Delays or backlogs in either can prevent a smooth, successful update.    

For database replication, you can use the Replication Link Analyzer to help resolve issues prior to starting the update.    

 For more information, see [About the Replication Link Analyzer](monitor-replication.md#BKMK_RLA).  

 **Install all applicable critical updates  for operating systems on computers that host the site, the site database server, and remote site system roles:** Before you install an update for Configuration Manager, install any critical updates for each applicable site system. If an update that you install requires a restart, restart the applicable computers before you start the upgrade.  

 **Disable database replicas for management points at primary sites:** Configuration Manager cannot successfully update a primary site that has a database replica for management points enabled. Disable database replication before you:  

-   Create a backup of the site database to test the database upgrade.  

-   Install an update for Configuration Manager.  

For more information, see   [Database replicas for management points for Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Reconfigure software update points that use NLBs:** Configuration Manager cannot update a site that uses a Network Load Balancing (NLB) cluster to host software update points.  If you use NLB clusters for software update points, use Windows PowerShell to remove the NLB cluster.    

 For more information, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md).  

 **Disable all site maintenance tasks at each site for the duration of the update installation on that site:** Before you install updates, disable any site maintenance task that might run during the time the update process is active. These tasks include (but are not limited) to the following:  

-   Backup Site Server  

-   Delete Aged Client Operations  

-   Delete Aged Discovery Data  

When a site database maintenance task runs during the update installation, the update installation can fail. Before you disable a task, record the schedule of the task so you can restore its configuration after the update has installed.  

 For more information, see [Maintenance tasks for Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) and [Reference for maintenance tasks for Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Temporarily stop any antivirus software on the Configuration Manager servers:** 
Before you update a site, ensure that you have stopped antivirus software on the Configuration Manager servers. <!--SMS.503481--> 

 **Create a backup of the site database at the central administration site and primary sites:** Before you update a site, backup the site database to ensure that you have a successful backup to use for disaster recovery.   

For more information, see [Backup and recovery for Configuration Manager](backup-and-recovery.md).  

 **Backup a customized Configuration.mof file:** If you use a customized Configuration.mof file to define data classes that you use with hardware inventory, create a backup of this file before updating the site. After the update, restore this file to your version 1602 site. When you update a site, the current file is overwritten with the original (default) version of the file. For more information about using this file, see [How to extend hardware inventory](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

-   You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   
Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable.

 **Plan for client piloting:** When you install an update that updates the client, you can test that new client update in pre-production before it deploys and upgrades all your active clients.   

 To take advantage of this option, you must configure your site to support automatic upgrades for pre-production before beginning installation of the update. For more information, see [Upgrade clients](../../../core/clients/manage/upgrade/upgrade-clients.md) and   
[How to test client upgrades in a pre-production collection](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Plan to use Maintenance windows to control when site servers install updates:** You can use the maintenance windows to define a period of time during which updates to the site server can be installed. This can help you control when sites in your hierarchy install the update.   

Beginning with the release of the 1602 update, maintenance windows have been renamed *service windows*. For more information, see [Service windows for site servers](service-windows.md).  

 **Run setup prerequisite checker:**  Before you install update 1602, you can run the prerequisite checker independently from the update installation. When you install the update on the site, prerequisite checker runs again.  

For more information, see **Step 3: Run the prerequisite checker before installing an update** in the [Updates for Configuration Manager](../../../core/servers/manage/updates.md) topic.  

> [!IMPORTANT]  
>  When the prerequisite checker runs independently or as part of an update installation, the process updates some product source files that are used for site maintenance tasks. Therefore, after running the prerequisite checker but before installing the 1602 update, if you need to perform a site maintenance task, run **Setupwfe.exe** (Configuration Manager Setup) from the CD.Latest folder on the site server.  

 **Update sites:** You are now ready to start the update installation for your hierarchy. We recommend that you plan to install the update outside of normal business hours for each site, when the process of installing the update and its actions to reinstall site components and site system roles will have the least effect on your business operations.

For more information, see [Updates for Configuration Manager](../../../core/servers/manage/updates.md).  

## See also  
 [Updates for Configuration Manager](../../../core/servers/manage/updates.md)
