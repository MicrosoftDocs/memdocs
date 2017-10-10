---
title: "Checklist for 1606"
description: "Learn about actions to take before updating from System Center Configuration Manager version 1511 or 1602 to version 1606."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Checklist for installing update 1606 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Version 1606 for System Center Configuration Manager current branch is an update that you can use to update from version 1511 or 1602.

Before installing version 1606 as an update, review the following information and checklist for actions to take before starting the update.

For information about baseline versions, see [Baseline and update versions](../../../core/servers/manage/updates.md#bkmk_Baselines) in [Updates for System Center Configuration Manager](../../../core/servers/manage/updates.md).

 ## About installing update 1606

As an *update*, 1606 can only be installed at the top-level site of your hierarchy. This means you initiate the installation from your central administration site if you have one, or from your stand-alone primary site.  

-   Child primary sites install the update automatically after the central administration site finishes installing the update. You can use service windows to control when a site installs updates. Prior to version 1606, service windows were called maintenance windows. For more information, see [Service windows for site servers](/sccm/core/servers/manage/service-windows).  

-   You must manually update secondary sites from within the Configuration Manager console after the primary parent site finishes installing the update. Automatic update of secondary site servers is not supported.  

When the site server installs the update, site system roles that are installed on the site server and those that are installed on remote computers get updated automatically. Therefore, before installing the update, make sure that each site system server meets any new prerequisites for operations with the new update version.  

The first time you use a Configuration Manager console after the update has been installed, you will be prompted to update that console.  To do so, you must run Configuration Manager setup on the computer that hosts the console, and then choose the option to update the console. We recommend that you do not delay installing the update to the console.

 **Known issues for this update**   
  The following issues apply when you view the update pack installation status:
  - When updating from version 1602 to 1606, the step **Extract update package payload** displays a Status of **Not started**, even though the download has completed.
  - When updating from version 1511 to 1606, some steps will show a status of **Completed** but will not display a value for **Last Update Time**.


## Checklist  

 **Ensure that all sites run a supported version of System Center Configuration Manager:**  Before you start the installation of update 1606, each site server in the hierarchy must run the same version of System Center Configuration Manager: either version 1511 or 1602.

 **Review installed Microsoft.NET versions on site system servers:** When a site installs update 1606, Configuration Manager automatically installs .NET Framework 4.5.2 on each computer that hosts one of the following site system roles (if .NET Framework 4.5 or later is not already installed):  

-   Enrollment proxy point  

-   Enrollment point  

-   Management point  

-   Service connection point  

This installation can put the site system server into a reboot pending state and report errors to the Configuration Manager component status viewer. Additionally, .NET applications on the server might have random failures until the server is rebooted.  

 For more information see [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Review the site and hierarchy status and verify that there are no unresolved issues:** Before you update a site, resolve all operational issues for the site server, the site database server, and site system roles that are installed on remote computers. A site update can fail due to existing operational problems.

 For more information, see [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Review file and data replication between sites:**  Ensure that file and database replication between sites is operational and current. Delays or backlogs in either can prevent a smooth, successful update.    

For database replication, you can use the Replication Link Analyzer to help resolve issues prior to starting the update. For more information, see   [About the Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) in the topic [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Install all applicable critical updates  for operating systems on computers that host the site, the site database server, and remote site system roles:** Before you install an update for Configuration Manager, install any critical updates for each applicable site system. If an update that you install requires a restart, restart the applicable computers before you start the upgrade.  

 **Disable database replicas for management points at primary sites:** Configuration Manager cannot successfully update a primary site that has a database replica for management points enabled. Disable database replication before you install an update for Configuration Manager.  

For more information, see   [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Set SQL Server AlwaysOn availability groups to manual failover:**  
 Before installing updates, such as version 1606, ensure that the availability group is set to manual failover. After the site has been updated, you can restore failover to be automatic. For more information, see [SQL Server AlwaysOn for a site database](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Reconfigure software update points that use NLBs:** Configuration Manager cannot update a site that uses a Network Load Balancing (NLB) cluster to host software update points.  

If you use NLB clusters for software update points, use Windows PowerShell to remove the NLB cluster.    

 For more information, see [Plan for software updates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Disable all site maintenance tasks at each site for the duration of the update installation on that site:** Before you install the update, disable any site maintenance tasks that might run during the time that the update process is active. This includes but is not limited to the following:  

-   Backup Site Server  

-   Delete Aged Client Operations  

-   Delete Aged Discovery Data  

When a site database maintenance task runs during the update installation, the update installation can fail. Before you disable a task, record the schedule of the task so you can restore its configuration after the update has been installed.  

For more information, see [Maintenance tasks for System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) and [Reference for maintenance tasks for System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Create a backup of the site database at the central administration site and primary sites:** Before you update a site, back up the site database to ensure that you have a successful backup to use for disaster recovery.   

For more information, see [Backup and recovery for System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
 **Test the database upgrade on a copy of the most recent site database backup:** Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

-   You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

 **Plan for client piloting:** When you install an update that updates the client, you can test that new client update in pre-production before it deploys and upgrades all your active clients.   

 To take advantage of this option, before starting the installation of the update, you must configure your site to support automatic upgrades for pre-production. For more information, see [Upgrade clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) and   
[How to test client upgrades in a pre-production collection in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Plan to use service windows to control when site servers install updates:** You can use service windows to define a period during which updates to a site server can be installed.

This can help you control when sites in your hierarchy install the update.
Prior to version 1606, service windows were called maintenance windows. For more information, see [Service windows for site servers](/sccm/core/servers/manage/service-windows).  

 **Run setup prerequisite checker:**  Before you install update 1606, you can run the prerequisite checker independently from the update installation. When you install the update on the site, prerequisite checker runs again.  

For more information, see **Step 3: Run the prerequisite checker before installing an update** in the [Updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) topic.  

> [!IMPORTANT]  
>  When the prerequisite checker runs independently or as part of an update installation, the process updates some product source files that are used for site maintenance tasks. Therefore, after running the prerequisite checker but before installing the 1606 update, if you need to perform a site maintenance task, run **Setupwpf.exe** (Configuration Manager Setup) from the CD.Latest folder on the site server.  

 **Update sites:** You are now ready to start the update installation for your hierarchy.  
  We recommend that you plan to install the update outside of normal business hours for each site, when the process of installing the update and its actions to reinstall site components and site system roles will have the least effect on your business operations.

For more information, see [Updates for System Center Configuration Manager](../../../core/servers/manage/updates.md).  
