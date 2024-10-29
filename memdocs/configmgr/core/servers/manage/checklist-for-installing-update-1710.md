---
title: Checklist for 1710 | Configuration Manager
titleSuffix: Configuration Manager
description: Learn about actions to take before updating to Configuration Manager version 1710.
ms.date: 12/19/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Checklist for installing update 1710 for Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you use the current branch of Configuration Manager, you can install the in-console update for version 1710 to update your hierarchy from a previous version.

To get the update for version 1710, you must use a service connection point site system role at the top-level site of your hierarchy. This can be in online or offline mode. After your hierarchy downloads the update package from Microsoft, you can find it in the console under **Administration &gt; Overview &gt; Cloud Services &gt; Updates and Servicing**.

-   When the update is listed as **Available**, the update is ready to install. Before installing version 1710, review the following information [about installing update 1710](#about-installing-update-1710) and the [checklist](#checklist) for configurations to make before starting the update.

-   If the update displays as **Downloading** and does not change, review the **hman.log** and **dmpdownloader.log** for errors.

    -   If the dmpdownloader.log indicates the dmpdownloader process is asleep and waiting for an interval before checking for updates, you can restart the **SMS_Executive** service on the site server to restart the download of the update's redistribution files.

    -   Another common download issue occurs when proxy server settings prevent downloads from `silverlight.dlservice.microsoft.com` and `download.microsoft.com`.

For more information about installing updates, see [In-console updates and servicing](updates.md#bkmk_inconsole).

For information about the versions of the Current Branch, see [Baseline and update versions](updates.md#bkmk_Baselines) in [Updates for Configuration Manager](updates.md).

## About installing update 1710

**Sites:**  
You install update 1710 at the top-level site of your hierarchy. This means you initiate the installation from your central administration site if you have one, or from your stand-alone primary site. After the update is installed at the top-tier site, child sites have the following update behavior:

-   Child primary sites install the update automatically after the central administration site finishes the installation of the update. You can use service windows to control when a site installs the update. For more information, see [Service windows for site servers](service-windows.md).

-   You must manually update each secondary site from within the Configuration Manager console after the primary parent site finishes the update installation. Automatic update of secondary site servers is not supported.

**Site system roles:**  
When a site server installs the update, the site system roles that are installed on the site server computer, and those that are installed on remote computers, automatically get updated. Before installing the update, make sure that each site system server meets the prerequisites for operation with the new update version.

**Configuration Manager consoles:**   
The first time you use a Configuration Manager console after the update has finished, you will be prompted to update that console. To do so, you must run Configuration Manager setup on the computer that hosts the console, and then choose the option to update the console. We recommend that you do not delay installing the update to the console.

> [!IMPORTANT]  
> When you install an update at the central administration site, be aware of the following limitations and delays that exist until all child primary sites also complete the update installation:    
> - **Client upgrades** do not start. This includes automatic updates of clients and pre-production clients. Additionally, you cannot promote pre-production clients to production until the last site completes the update installation. After the last site completes the update installation, client upgrades will begin based on your configuration choices.   
> - **New features** you enable with the update are not available. This is to prevent the replication of data related to that feature from being sent to a site that has not yet installed support for that feature. After all primary sites install the update, the feature will be available for use.   
> - **Replication links** between the central administration site and child primary sites display as not upgraded. This displays in the update pack installation status as a status of Completed with warning for Monitoring replication initialization. In the Monitoring node of the console, this displays as *Link is being configured*.


## Checklist

**Ensure that all sites run a version of Configuration Manager that supports update to 1710:**   
Each site server in the hierarchy must run the same version of Configuration Manager before you can start the installation of update 1710. To update to 1710, you must use version 1610, 1702, or 1706.

**Review the status of your Software Assurance or equivalent subscription rights:**   
You must have an active Software Assurance (SA) agreement to install update 1710. When you install this update, the **Licensing** tab presents the option to confirm your **Software Assurance expiration date**.

This is an optional value that you can specify as a convenient reminder of your license expiration date. This date is visible when you install future updates. You might have previously specified this value during setup or installation of an update, or by using the **Licensing** tab of the **Hierarchy Settings**, from within the Configuration Manager console.

For more information, see [Licensing and branches for Configuration Manager](../../understand/learn-more-editions.md).

**Review installed Microsoft .NET versions on site system servers:** 
When a site installs this update, Configuration Manager automatically installs .NET Framework 4.5.2 on each computer that hosts one of the following site system roles when .NET Framework 4.5 or later is not already installed:

-   Enrollment proxy point
-   Enrollment point
-   Management point
-   Service connection point

This installation can put the site system server into a reboot pending state and report errors to the Configuration Manager component status viewer. Additionally, .NET applications on the server might experience random failures until the server is restarted.

For more information, see [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md).

**Review the version of the Windows Assessment and Deployment Kit (ADK) for Windows 10**
The Windows 10 ADK should be version 1703 or later. (For more information on supported Windows ADK versions, see [Windows ADK](../../plan-design/configs/support-for-windows-adk.md).) If you must update the Windows ADK, do so before you begin the update of Configuration Manager. This ensures the default boot images are automatically updated to the latest version of Windows PE. (Custom boot images must be updated manually.)

If you update the site before you update the Windows ADK, see [Update distribution points with the boot image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image) for improvements to this process in Configuration Manager version 1710.

**Review the site and hierarchy status and verify that there are no unresolved issues:** 
Before you update a site, resolve all operational issues for the site server, the site database server, and site system roles that are installed on remote computers. A site update can fail due to existing operational problems.

For more information, see [Use the status system](use-status-system.md).

**Review file and data replication between sites:**   
Ensure that file and database replication between sites is operational and current. Delays or backlogs in either can prevent a smooth, successful update.
For database replication, you can use the Replication Link Analyzer to help resolve issues prior to starting the update.

For more information, see [Replication Link Analyzer](monitor-replication.md#BKMK_RLA) in the [Monitor database replication](monitor-replication.md#BKMK_RLA) topic.

**Install all applicable critical updates for operating systems on computers that host the site, the site database server, and remote site system roles:** 
Before you install an update for Configuration Manager, install any critical updates for each applicable site system. If an update that you install requires a restart, restart the applicable computers before you start the upgrade.

**Disable database replicas for management points at primary sites:**   
Configuration Manager cannot successfully update a primary site that has a database replica for management points enabled. Disable database replication before you install an update for Configuration Manager.

For more information, see [Database replicas for management points for Configuration Manager](../deploy/configure/database-replicas-for-management-points.md).

**Set SQL Server Always On availability groups to manual failover:**   
If you use an availability group, ensure that the availability group is set to manual failover before you start the update installation. After the site has  updated, you can restore failover to be automatic. For more information see [Prepare to use an availability group](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Reconfigure software update points that use NLBs:**   
<!-- Support for NLBs is fully removed with 1702. When 1702 is no longer in support, this statement can drop -->
Configuration Manager cannot update a site that uses a network load balancing (NLB) cluster to host software update points.

If you use NLB clusters for software update points, use Windows PowerShell to remove the NLB cluster.
For more information, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md).

**Disable all site maintenance tasks at each site for the duration of the update installation on that site:**   
Before you install the update, disable any site maintenance task that might run during the time the update process is active. This includes but is not limited to the following:

-   Backup Site Server
-   Delete Aged Client Operations
-   Delete Aged Discovery Data

When a site database maintenance task runs during the update installation, the update installation can fail. Before you disable a task, record the schedule of the task so you can restore its configuration after the update has been installed.

For more information, see [Maintenance tasks for Configuration Manager](maintenance-tasks.md) and [Reference for maintenance tasks for Configuration Manager](reference-for-maintenance-tasks.md).

**Temporarily stop any antivirus software on the Configuration Manager servers:** 
Before you update a site, ensure that you have stopped antivirus software on the Configuration Manager servers. <!--SMS.503481--> 

**Create a backup of the site database at the central administration site and primary sites:** 
Before you update a site, back up the site database to ensure that you have a successful backup to use for disaster recovery.

For more information, see [Backup and recovery for Configuration Manager](backup-and-recovery.md).

**Plan for client piloting:**   
When you install an update that updates the client, you can test that new client update in pre-production before it deploys and upgrades all your active clients.

To take advantage of this option, you must configure your site to support automatic upgrades for pre-production before beginning installation of the update.

For more information, see [Upgrade clients](../../clients/manage/upgrade/upgrade-clients.md) and [How to test client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md).

**Plan to use service windows to control when site servers install updates:**   
Use service windows to define a period during which updates to a site server can be installed.

This can help you control when sites in your hierarchy install the update. For more information, see [Service windows for site servers](service-windows.md).

**Run the setup prerequisite checker:**   
When the update is listed in the console as **Available,** you can independently run the prerequisite checker before installing the update. (When you install the update on the site, prerequisite checker runs again.)

To run a prerequisite check from the console, go to **Administration > Overview > Cloud Services > Updates and Servicing.** Next, right-click  **Configuration Manager 1710 update package**, and then choose **Run prerequisite check**.

For more information about starting and then monitoring the prerequisite check, see **Step 3: Run the prerequisite checker before installing an update** in the topic [Install in-console updates for Configuration Manager](install-in-console-updates.md).

> [!IMPORTANT]  
> When the prerequisite checker runs independently or as part of an update installation, the process updates some product source files that are used for site maintenance tasks. Therefore, after running the prerequisite checker but before installing the update, if you need to perform a site maintenance task, run **Setupwpf.exe** (Configuration Manager Setup) from the CD.Latest folder on the site server.

**Update sites:**   
You are now ready to start the update installation for your hierarchy. For more information about installing the update, see [Install in-console updates.](install-in-console-updates.md).

We recommend that you plan to install the update outside of normal business hours for each site when the process of installing the update and its actions to reinstall site components and site system roles will have the least effect on your business operations.

For more information, see [Updates for Configuration Manager](updates.md).

## Post update Checklist
Review the following actions to take after the update installation is finished.
1. Make sure that site-to-site replication is active. In the console, view **Monitoring** > **Site Hierarchy**, and **Monitoring** > **Database Replication** for indications of problems or confirmation that replication links are active.
2. Make sure each site server and site system role has updated to version 1710. In the console, you can add the optional column **Version** to the display of some nodes including **Sites** and **Distribution Points**.

   When necessary, a site system role will reinstall automatically to update to the new version. Consider restarting remote site systems that do not update successfully.
3. Reconfigure database replicas for management points at primary sites that you disabled before starting the update.
4. Reconfigure database maintenance tasks that you disabled before starting the update.
5. If you configured client piloting before installing the update, upgrade clients per the plan you created.
