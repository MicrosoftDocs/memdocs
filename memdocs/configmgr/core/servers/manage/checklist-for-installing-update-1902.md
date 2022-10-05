---
title: Checklist for 1902
titleSuffix: Configuration Manager
description: Learn about actions to take before updating to Configuration Manager version 1902.
ms.date: 04/11/2019
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

# Checklist for installing update 1902 for Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you use the current branch of Configuration Manager, you can install the in-console update for version 1902 to update your hierarchy from a previous version. <!-- baseline only statement:-->(Because version 1902 is also available as [baseline media](updates.md#bkmk_Baselines), you can use the installation media to install the first site of a new hierarchy.)

To get the update for version 1902, you must use a service connection point at the top-level site of your hierarchy. This site system role can be in online or offline mode. After your hierarchy downloads the update package from Microsoft, find it in the console. In the **Administration** workspace, select the **Updates and Servicing** node.

-   When the update is listed as **Available**, the update is ready to install. Before installing version 1902, review the following information [about installing update 1902](#about-installing-update-1902) and the [checklist](#checklist) for configurations to make before starting the update.

-   If the update displays as **Downloading** and doesn't change, review the **hman.log** and **dmpdownloader.log** for errors.

    -   The dmpdownloader.log may indicate that the dmpdownloader process is waiting for an interval before checking for updates. To restart the download of the update's redistribution files, restart the **SMS_Executive** service on the site server.

    -   Another common download issue occurs when proxy server settings prevent downloads from `silverlight.dlservice.microsoft.com`, `download.microsoft.com`, and `go.microsoft.com`.

For more information about installing updates, see [In-console updates and servicing](updates.md#bkmk_inconsole).

For more information about current branch versions, see [Baseline and update versions](updates.md#bkmk_Baselines).



## About installing update 1902

#### Sites
You install update 1902 at the top-level site of your hierarchy. Start the installation from your central administration site or from your stand-alone primary site. After the update is installed at the top-level site, child sites have the following update behavior:

-   Child primary sites install the update automatically after the central administration site finishes the installation of the update. You can use service windows to control when a site installs the update. For more information, see [Service windows for site servers](service-windows.md).

-   Manually update each secondary site from within the Configuration Manager console after the primary parent site finishes the update installation. Automatic update of secondary site servers isn't supported.

#### Site system roles
When a site server installs the update, it automatically updates all of the site system roles. These roles are on the site server or  installed on remote servers. Before installing the update, make sure that each site system server meets the current prerequisites for the new update version.

#### Configuration Manager consoles   
The first time you use a Configuration Manager console after the update has finished, you're prompted to update that console. You can also run the Configuration Manager setup on the computer that hosts the console, and choose the option to update the console. Install the update to the console as soon as possible. For more information, see [Install the Configuration Manager console](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> When you install an update at the central administration site, be aware of the following limitations and delays that exist until all child primary sites also complete the update installation:    
> - **Client upgrades** do not start. This includes automatic updates of clients and pre-production clients. Additionally, you cannot promote pre-production clients to production until the last site completes the update installation. After the last site completes the update installation, client upgrades will begin based on your configuration choices.   
> - **New features** you enable with the update are not available. This is to prevent the replication of data related to that feature from being sent to a site that has not yet installed support for that feature. After all primary sites install the update, the feature will be available for use.   
> - **Replication links** between the central administration site and child primary sites display as not upgraded. This displays in the update pack installation status as a status of Completed with warning for Monitoring replication initialization. In the Monitoring node of the console, this displays as *Link is being configured*.


## Checklist

#### All sites run a supported version of Configuration Manager  
Each site server in the hierarchy must run the same version of Configuration Manager before you can start the installation of update 1902. To update to 1902, you must use version 1802, 1806, or 1810.

#### Review the status of your product licensing 
You must have an active Software Assurance (SA) agreement or equivalent subscription rights to install this update. When you update the site, the **Licensing** page presents the option to confirm your **Software Assurance expiration date**.

This value is optional. You can specify as a convenient reminder of your license expiration date. This date is visible when you install future updates. You might have previously specified this value during setup or installation of an update. You can also specify this value in the Configuration Manager console. In the **Administration** workspace, expand **Site Configuration**, and select **Sites**. Select **Hierarchy Settings** in the ribbon, and switch to the **Licensing** tab.

For more information, see [Licensing and branches](../../understand/learn-more-editions.md).

#### Review Microsoft .NET versions 
When a site installs this update, if the minimum requirement of .NET Framework 4.5 is not installed, Configuration Manager automatically installs .NET Framework 4.5.2. When this prerequisite isn't already installed, the site installs it on each server that hosts one of the following site system roles:

-   Management point
-   Service connection point
-   Enrollment proxy point
-   Enrollment point

This installation can put the site system server into a reboot pending state and report errors to the Configuration Manager component status viewer. Additionally, .NET applications on the server might experience random failures until the server is restarted.

For more information, see [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md).

#### Review the version of the Windows ADK for Windows 10
The version of the Windows 10 Assessment and Deployment Kit (ADK) should be supported for Configuration Manager version 1902. For more information on supported Windows ADK versions, see [Windows 10 ADK](../../plan-design/configs/support-for-windows-adk.md). If you need to update the Windows ADK, do so before you begin the update of Configuration Manager. This order makes sure the default boot images are automatically updated to the latest version of Windows PE. Manually update any custom boot images after updating the site.

If you update the site before you update the Windows ADK, see [Update distribution points with the boot image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

#### Review SQL Server Native Client version
A minimum version of SQL Server 2012 Native Client which includes support for TLS 1.2 must be installed. For more information, see the [List of prerequisite checks](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

#### Review the site and hierarchy status for unresolved issues 
A site update can fail due to existing operational problems. Before you update a site, resolve all operational issues for the following systems:  
- The site server  
- The site database server  
- Remote site system roles on other servers   

For more information, see [Use the status system](use-status-system.md).

#### Review file and data replication between sites   
Make sure that file and database replication between sites is operational and current. Delays or backlogs in either can prevent a smooth, successful update. For database replication, you can use the Replication Link Analyzer to help resolve issues prior to starting the update.

For more information, see [About the Replication Link Analyzer](monitor-replication.md#BKMK_RLA).

#### Install all applicable critical Windows updates
Before you install an update for Configuration Manager, install any critical OS updates for each applicable site system. These servers include the site server, site database server, and remote site system roles. If an update that you install requires a restart, restart the applicable servers before you start the upgrade.

#### Disable database replicas for management points at primary sites   
Configuration Manager can't successfully update a primary site that has a database replica for management points enabled. Before you install an update for Configuration Manager, disable database replication.

For more information, see [Database replicas for management points](../deploy/configure/database-replicas-for-management-points.md).

#### Set SQL Server Always On availability groups to manual failover   
If you use an availability group, make sure that the availability group is set to manual failover before you start the update installation. After the site has updated, you can restore failover to be automatic. For more information, see [Prepare to use an availability group](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

#### Disable site maintenance tasks at each site
Before you install the update, disable any site maintenance task that might run during the time the update process is active. For example, but not limited to:

-   Backup Site Server
-   Delete Aged Client Operations
-   Delete Aged Discovery Data

When a site database maintenance task runs during the update installation, the update installation can fail. Before you disable a task, record the schedule of the task so you can restore its configuration after the update has been installed.

For more information, see [Maintenance tasks](maintenance-tasks.md) and [Reference for maintenance tasks](reference-for-maintenance-tasks.md).

#### Temporarily stop any antivirus software 
Before you update a site, stop antivirus software on the Configuration Manager servers. The antivirus software can lock some files that need to be updated which causes our update to fail. <!--SMS.503481--> 

#### Create a backup of the site database 
Before you update a site, back up the site database at the central administration site and primary sites. This backup makes sure you have a successful backup to use for disaster recovery.

For more information, see [Backup and recovery](backup-and-recovery.md).

#### Plan for client piloting   
When you install an update that updates the client, you can test that new client update in pre-production before it deploys and upgrades all your active clients. To take advantage of this option, you must configure your site to support automatic upgrades for pre-production before beginning installation of the update.

For more information, see [Upgrade clients](../../clients/manage/upgrade/upgrade-clients.md) and [How to test client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md).

#### Plan to use service windows   
To define a period during which updates to a site server can be installed, use service windows. They can help you control when sites in your hierarchy install the update. For more information, see [Service windows for site servers](service-windows.md).

#### Review supported extensions
<!--SCCMdocs#587-->
If you extend Configuration Manager with other products from Microsoft or Microsoft partners, confirm that those products support version 1902. Check with the product vendor for this information. For example, see the Microsoft Deployment Toolkit [release notes](../../../mdt/release-notes.md).

#### Run the setup prerequisite checker   
When the update is listed in the console as **Available,** you can independently run the prerequisite checker before installing the update. (When you install the update on the site, prerequisite checker runs again.)

To run a prerequisite check from the console, go to the **Administration** workspace, and select **Updates and Servicing**. Select the **Configuration Manager 1902** update package, and select **Run prerequisite check** in the ribbon.

For more information, see the section to **Run the prerequisite checker before installing an update** in [Before you install an in-console update](prepare-in-console-updates.md#before-you-install-an-in-console-update).

> [!IMPORTANT]  
> When the prerequisite checker runs, the process updates some product source files that are used for site maintenance tasks. Therefore, after running the prerequisite checker but before installing the update, if you need to perform a site maintenance task, run **Setupwpf.exe** (Configuration Manager Setup) from the CD.Latest folder on the site server.

#### Update sites   
You're now ready to start the update installation for your hierarchy. For more information about installing the update, see [Install in-console updates](install-in-console-updates.md).

You may plan to install the update outside of normal business hours. Determine when the process will have the least effect on your business operations. Installing the update and its actions reinstall site components and site system roles.

For more information, see [Updates for Configuration Manager](updates.md).



## Post-update checklist

After the site updates, use the following checklist to complete common tasks and configurations.


#### Confirm version and restart (if necessary)
Make sure each site server and site system role has updated to version 1902. In the console, add the **Version** column to the **Sites** and **Distribution Points** nodes in the **Administration** workspace. When necessary, a site system role automatically reinstalls to update to the new version. 

Consider restarting remote site systems that don't successfully update at first. Review your site infrastructure and make sure that applicable site servers and remote site system servers have restarted successfully. Typically, site servers restart only when Configuration Manager installs .NET as a prerequisite for a site system role.


#### Confirm site-to-site replication is active
In the Configuration Manager console, go to the following locations to view the status, and make sure that replication is active:  

-   **Monitoring** workspace, **Site Hierarchy** node  

-   **Monitoring** workspace, **Database Replication** node  

For more information, see the following articles:  

- [Monitor hierarchy](monitor-hierarchy.md)
- [Monitor replication](monitor-replication.md)
- [About the Replication Link Analyzer](monitor-replication.md#BKMK_RLA)  


#### Update Configuration Manager consoles
Update all remote Configuration Manager consoles to the same version. You're prompted to update the console when:  

-   You open the console.  

-   You go to a new node in the console.  


#### Reconfigure database replicas for management points
After you update a primary site, reconfigure the database replica for management points that you uninstalled before you updated the site. For more information, see [Database replicas for management points](../deploy/configure/database-replicas-for-management-points.md).  


#### Reconfigure any disabled maintenance tasks
If you disabled database [maintenance tasks](maintenance-tasks.md) at a site before installing the update, reconfigure those tasks. Use the same settings that were in place before the update.  


#### Update clients
Update clients per the plan you created, especially if you configured client piloting before installing the update. For more information, see [How to upgrade clients for Windows computers](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  


#### Third-party extensions
If you use any extensions to Configuration Manager, update them to the latest version to support Configuration Manager version 1902. 


#### Update custom boot images and media
<!--SCCMDocs issue 775-->

Use the **Update Distribution Points** action for any boot image that you use, whether it's a default or custom boot image. This action makes sure that clients can use the latest version. Even if there isn't a new version of the Windows ADK, the Configuration Manager client components may change with an update. If you don't update boot images and media, task sequence deployments may fail on devices. 

When you update the site, Configuration Manager automatically updates the *default* boot images. It doesn't automatically distribute the updated content to distribution points. Use the **Update Distribution Points** action on specific boot images when you're ready to distribute this content across your network. 

After updating the site, manually update any *custom* boot images. This action updates the boot image with the latest client components if necessary, optionally reloads it with the current Windows PE version, and redistributes the content to the distribution points. 

For more information, see [Update distribution points with the boot image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image). 
