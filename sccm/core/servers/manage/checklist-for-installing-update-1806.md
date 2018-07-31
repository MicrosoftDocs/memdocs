---
title: Checklist for 1806
titleSuffix: Configuration Manager
description: Learn about actions to take before updating to Configuration Manager version 1806.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb0a87a6-fd65-440b-90a5-2fef35622c9d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Checklist for installing update 1806 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When you use the current branch of System Center Configuration Manager, you can install the in-console update for version 1806 to update your hierarchy from a previous version. <!-- baseline only statement: (Because version 1802 is also available as [baseline media](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions), you can use the installation media to install the first site of a new hierarchy.)-->

To get the update for version 1806, you must use a service connection point at the top-level site of your hierarchy. This site system role can be in online or offline mode. After your hierarchy downloads the update package from Microsoft, find it in the console. In the **Administration** workspace, select the **Updates and Servicing** node.

-   When the update is listed as **Available**, the update is ready to install. Before installing version 1806, review the following information [about installing update 1806](#about-installing-update-1806) and the [checklist](#checklist) for configurations to make before starting the update.

-   If the update displays as **Downloading** and doesn't change, review the **hman.log** and **dmpdownloader.log** for errors.

    -   The dmpdownloader.log may indicate that the dmpdownloader process is waiting for an interval before checking for updates. To restart the download of the update's redistribution files, restart the **SMS_Executive** service on the site server.

    -   Another common download issue occurs when proxy server settings prevent downloads from http://silverlight.dlservice.microsoft.com and http://download.microsoft.com.

For more information about installing updates, see [In-console updates and servicing](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

For more information about current branch versions, see [Baseline and update versions](/sccm/core/servers/manage/updates#bkmk_Baselines).



## About installing update 1806

#### Sites
You install update 1806 at the top-level site of your hierarchy. Start the installation from your central administration site or from your stand-alone primary site. After the update is installed at the top-level site, child sites have the following update behavior:

-   Child primary sites install the update automatically after the central administration site finishes the installation of the update. You can use service windows to control when a site installs the update. For more information, see [Service windows for site servers](/sccm/core/servers/manage/service-windows).

-   Manually update each secondary site from within the Configuration Manager console after the primary parent site finishes the update installation. Automatic update of secondary site servers isn't supported.

#### Site system roles
When a site server installs the update, it automatically updates all of the site system roles. These roles are on the site server or  installed on remote servers. Before installing the update, make sure that each site system server meets the current prerequisites for the new update version.

#### Configuration Manager consoles   
The first time you use a Configuration Manager console after the update has finished, you're prompted to update that console. You can also run the Configuration Manager setup on the computer that hosts the console, and choose the option to update the console. Install the update to the console as soon as possible. For more information, see [Install the Configuration Manager console](/sccm/core/servers/deploy/install/install-consoles).

> [!IMPORTANT]  
> When you install an update at the central administration site, be aware of the following limitations and delays that exist until all child primary sites also complete the update installation:    
> - **Client upgrades** do not start. This includes automatic updates of clients and pre-production clients. Additionally, you cannot promote pre-production clients to production until the last site completes the update installation. After the last site completes the update installation, client upgrades will begin based on your configuration choices.   
> - **New features** you enable with the update are not available. This is to prevent the replication of data related to that feature from being sent to a site that has not yet installed support for that feature. After all primary sites install the update, the feature will be available for use.   
> - **Replication links** between the central administration site and child primary sites display as not upgraded. This displays in the update pack installation status as a status of Completed with warning for Monitoring replication initialization. In the Monitoring node of the console, this displays as *Link is being configured*.


## Checklist

#### All sites run a supported version of Configuration Manager  
Each site server in the hierarchy must run the same version of Configuration Manager before you can start the installation of update 1806. To update to 1806, you must use version 1706, 1710, or 1802.

#### Review the status of your product licensing 
You must have an active Software Assurance (SA) agreement or equivalent subscription rights to install this update. When you update the site, the **Licensing** page presents the option to confirm your **Software Assurance expiration date**.

This value is optional. You can specify as a convenient reminder of your license expiration date. This date is visible when you install future updates. You might have previously specified this value during setup or installation of an update. You can also specify this value in the Configuration Manager console. In the **Administration** workspace, expand **Site Configuration**, and select **Sites**. Click **Hierarchy Settings** in the ribbon, and switch to the **Licensing** tab.

For more information, see [Licensing and branches](/sccm/core/understand/learn-more-editions).

#### Review Microsoft .NET versions 
When a site installs this update, Configuration Manager automatically installs .NET Framework 4.5.2. When this prerequisite isn't already installed, the site installs it on each server that hosts one of the following site system roles:

-   Management point
-   Service connection point
-   Enrollment proxy point
-   Enrollment point

This installation can put the site system server into a reboot pending state and report errors to the Configuration Manager component status viewer. Additionally, .NET applications on the server might experience random failures until the server is restarted.

For more information, see [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

#### Review the version of the Windows ADK for Windows 10
The version of the Windows 10 Assessment and Deployment Kit (ADK) should be supported for Configuration Manager version 1806. For more information on supported Windows ADK versions, see [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk). If you need to update the Windows ADK, do so before you begin the update of Configuration Manager. This order ensures the default boot images are automatically updated to the latest version of Windows PE. Manually update any custom boot images after updating the site.

If you update the site before you update the Windows ADK, see [Update distribution points with the boot image](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

#### Review the site and hierarchy status for unresolved issues 
Before you update a site, resolve all operational issues for the site server, the site database server, and site system roles that are installed on remote computers. A site update can fail due to existing operational problems.

For more information, see [Use alerts and the status system](/sccm/core/servers/manage/use-alerts-and-the-status-system).

#### Review file and data replication between sites   
Ensure that file and database replication between sites is operational and current. Delays or backlogs in either can prevent a smooth, successful update. For database replication, you can use the Replication Link Analyzer to help resolve issues prior to starting the update.

For more information, see [About the Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA).

#### Install all applicable critical Windows updates
Before you install an update for Configuration Manager, install any critical OS updates for each applicable site system. These servers include the site server, site database server, and remote site system roles. If an update that you install requires a restart, restart the applicable servers before you start the upgrade.

#### Disable database replicas for management points at primary sites   
Configuration Manager can't successfully update a primary site that has a database replica for management points enabled. Before you install an update for Configuration Manager, disable database replication.

For more information, see [Database replicas for management points](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

#### Set SQL Server AlwaysOn availability groups to manual failover   
If you use an availability group, ensure that the availability group is set to manual failover before you start the update installation. After the site has updated, you can restore failover to be automatic. For more information, see [SQL Server AlwaysOn for a site database](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

#### Disable site maintenance tasks at each site
Before you install the update, disable any site maintenance task that might run during the time the update process is active. For example, but not limited to:

-   Backup Site Server
-   Delete Aged Client Operations
-   Delete Aged Discovery Data

When a site database maintenance task runs during the update installation, the update installation can fail. Before you disable a task, record the schedule of the task so you can restore its configuration after the update has been installed.

For more information, see [Maintenance tasks](/sccm/core/servers/manage/maintenance-tasks) and [Reference for maintenance tasks](/sccm/core/servers/manage/reference-for-maintenance-tasks).

#### Temporarily stop any antivirus software 
Before you update a site, stop antivirus software on the Configuration Manager servers. <!--SMS.503481--> 

#### Create a backup of the site database 
Before you update a site, back up the site database at the central administration site and primary sites. This backup ensures that you have a successful backup to use for disaster recovery.

For more information, see [Backup and recovery](/sccm/protect/understand/backup-and-recovery).

#### Plan for client piloting   
When you install an update that updates the client, you can test that new client update in pre-production before it deploys and upgrades all your active clients. To take advantage of this option, you must configure your site to support automatic upgrades for pre-production before beginning installation of the update.

For more information, see [Upgrade clients](/sccm/core/clients/manage/upgrade/upgrade-clients) and [How to test client upgrades in a pre-production collection](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### Plan to use service windows   
To define a period during which updates to a site server can be installed, use service windows. They can help you control when sites in your hierarchy install the update. For more information, see [Service windows for site servers](/sccm/core/servers/manage/service-windows).

#### Review supported extensions
<!--SCCMdocs#587-->
If you extend Configuration Manager with other products from Microsoft or Microsoft partners, confirm that those products support version 1806. Check with the product vendor for this information. For example, see the Microsoft Deployment Toolkit [release notes](/sccm/mdt/release-notes).

#### Run the setup prerequisite checker   
When the update is listed in the console as **Available,** you can independently run the prerequisite checker before installing the update. (When you install the update on the site, prerequisite checker runs again.)

To run a prerequisite check from the console, go to the **Administration** workspace, and select **Updates and Servicing**. Select the **Configuration Manager 1806** update package, and click **Run prerequisite check** in the ribbon.

For more information, see the section to **Run the prerequisite checker before installing an update** in [Before you install an in-console update](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall).

> [!IMPORTANT]  
> When the prerequisite checker runs, the process updates some product source files that are used for site maintenance tasks. Therefore, after running the prerequisite checker but before installing the update, if you need to perform a site maintenance task, run **Setupwpf.exe** (Configuration Manager Setup) from the CD.Latest folder on the site server.

#### Update sites   
You're now ready to start the update installation for your hierarchy. For more information about installing the update, see [Install in-console updates](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

You may plan to install the update outside of normal business hours. Determine when the process will have the least effect on your business operations. Installing the update and its actions reinstall site components and site system roles.

For more information, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).



## Post-update checklist
After the site updates, review the following actions:

1.	For multi-site hierarchies, make sure that site-to-site replication is active. In the console, go to the **Site Hierarchy** and **Database Replication** nodes in the **Monitoring** workspace. These nodes provide indications of problems or confirmation that replication links are active.  

2.	Make sure each site server and site system role has updated to version 1806. In the console, add the **Version** column to the **Sites** and **Distribution Points** nodes in the **Administration** workspace. When necessary, a site system role automatically reinstalls to update to the new version. Consider restarting remote site systems that don't successfully update at first.  

3.	Reconfigure database replicas for management points at primary sites that you disabled before starting the update.  

4.  Reconfigure database maintenance tasks that you disabled before starting the update.  

5.	If you configured client piloting before installing the update, upgrade clients per the plan you created.

6.  If you use any extensions to Configuration Manager, update them to the latest version to support Configuration Manager version 1806. 
