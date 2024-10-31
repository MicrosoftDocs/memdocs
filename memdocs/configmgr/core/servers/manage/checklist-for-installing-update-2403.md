---
title: Checklist for 2403
titleSuffix: Configuration Manager
description: Learn about actions to take before updating to Configuration Manager version 2403.
ms.date: 05/06/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Checklist for installing update 2403 for Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you use the current branch of Configuration Manager, you can install the in-console update for version 2403 to update your hierarchy from a previous version. 

To get the update for version 2403, you must use a service connection point at the top-level site of your hierarchy. This site system role can be in online or offline mode. To download the update when your service connection point is offline, [use the service connection tool](use-the-service-connection-tool.md).<!-- SCCMDocs#1946 -->

After your hierarchy downloads the update package from Microsoft, find it in the console. In the **Administration** workspace, select the **Updates and Servicing** node.

- When the update is listed as **Available**, the update is ready to install. Before installing version 2403, review the following information [about installing update 2403](#about-installing-update-2403) and the [pre-update checklist](#pre-update-checklist) for configurations to make before starting the update.

- If the update displays as **Downloading** and doesn't change, review the **hman.log** and **dmpdownloader.log** for errors.

  - The dmpdownloader.log may indicate that the dmpdownloader process is waiting for an interval before checking for updates. To restart the download of the update's redistribution files, restart the **SMS_Executive** service on the site server.

  - Another common download issue occurs when proxy server settings prevent downloads from [required internet endpoints](../../plan-design/network/internet-endpoints.md#updates-and-servicing).

For more information about installing updates, see [In-console updates and servicing](updates.md#bkmk_inconsole).

For more information about current branch versions, see [Baseline and update versions](updates.md#bkmk_Baselines).

## About installing update 2403

### Sites

Install update 2403 at the top-level site of your hierarchy. Start the installation from your central administration site (CAS) or from your stand-alone primary site. After the update is installed at the top-level site, child sites have the following update behavior:

- Child primary sites install the update automatically after the CAS finishes the installation of the update. You can use service windows to control when a site installs the update. For more information, see [Service windows for site servers](service-windows.md).

- Manually update each secondary site from within the Configuration Manager console after the primary parent site finishes the update installation. Automatic update of secondary site servers isn't supported.

### Site system roles

When a site server installs the update, it automatically updates all of the site system roles. These roles are on the site server or installed on remote servers. Before installing the update, make sure that each site system server meets the current prerequisites for the new update version.

### Configuration Manager consoles

The first time you use a Configuration Manager console after the update has finished, you're prompted to update that console. You can also run the Configuration Manager setup on the computer that hosts the console, and choose the option to update the console. Install the update to the console as soon as possible. For more information, see [Install the Configuration Manager console](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> When you install an update at the CAS, be aware of the following limitations and delays that exist until all child primary sites also complete the update installation:
>
> - **Client upgrades** don't start. This includes automatic updates of clients and pre-production clients. Additionally, you can't promote pre-production clients to production until the last site completes the update installation. After the last site completes the update installation, client updates begin based on your configuration choices.
> - **New features** you enable with the update aren't available. This behavior is to prevent the CAS replicating data related to that feature to a site that hasn't yet installed support for that feature. After all primary sites install the update, the feature is available for use.
> - **Replication links** between the CAS and child primary sites display as not upgraded. This state displays in the update installation status as *Completed with warning* for monitoring replication initialization. In the **Monitoring** workspace of the console, this state displays as *Link is being configured*.

### Early update ring

<!-- SCCMDocs#1397 -->

As of May 06 , 2024, version 2403 is globally available for all customers to install. If you previously opted in to the early update ring, watch for an update to this current branch version.

## Pre-update checklist

### All sites run a supported version of Configuration Manager

Each site server in the hierarchy must run the same version of Configuration Manager before you can start the installation. To update to version 2403, use version 2211 or later.

### Review the status of your product licensing

You need an active Software Assurance (SA) agreement or equivalent subscription rights to install this update. When you update the site, the **Licensing** page presents the option to confirm your **Software Assurance expiration date**.

This value is optional. You can specify as a convenient reminder of your license expiration date. This date is visible when you install future updates. You might have previously specified this value during setup or installation of an update. You can also specify this value in the Configuration Manager console. In the **Administration** workspace, expand **Site Configuration**, and select **Sites**. Select **Hierarchy Settings** in the ribbon, and switch to the **Licensing** tab.

For more information, see [Licensing and branches](../../understand/learn-more-editions.md).

### Review Microsoft .NET versions

Configuration Manager now requires Microsoft .NET Framework version 4.8 for site servers, specific site systems, clients, and the console.<!--10402814--> Before you run setup to install or update the site, first update .NET and restart the system.

This installation can put the site system server into a reboot pending state and report errors to the Configuration Manager component status viewer. .NET applications on the server might experience random failures until you restart the server.

For more information including how to manage restarts, see [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md#net-version-requirements).

### Review the version of the Windows ADK

The version of the Windows Assessment and Deployment Kit (ADK) should be supported for Configuration Manager version 2403. For more information, see [Support for the Windows ADK](../../plan-design/configs/support-for-windows-adk.md). If you need to update the Windows ADK, do so before you begin the update of Configuration Manager. This order makes sure the default boot images are automatically updated to the latest version of Windows PE. Manually update any custom boot images after updating the site.

If you update the site before you update the Windows ADK, see [Update distribution points with the boot image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

### Review SQL Server Native Client version

Install a minimum version of SQL Server 2012 Native Client, which includes support for TLS 1.2. For more information, see the [List of prerequisite checks](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

### Review SQL ODBC driver for CM

Starting with version 2309 and later, Configuration Manager requires the installation of the ODBC driver for SQL server as a prerequisite. This prerequisite is required when you create a new site or update an existing one.

### Review the site and hierarchy status for unresolved issues

A site update can fail because of existing operational problems. Before you update a site, resolve all operational issues for the following systems:  

- The site server  
- The site database server  
- Remote site system roles on other servers

For more information, see [Use the status system](use-status-system.md).

### Review file and data replication between sites

Make sure that file and database replication between sites is operational and current. Delays or backlogs in either can prevent a successful update.

#### Database replication

For [database replication](../../plan-design/hierarchy/database-replication.md), to help resolve issues before you start the update, use the **Replication Link Analyzer** (RLA). For more information, see [Monitor database replication](monitor-replication.md).

Use RLA to answer the following questions:

- Is replication per group in a good state?
- Are any links degraded?
- Are there any errors?

If there's a backlog, wait until it clears out. If the backlog is large, such as millions of records, then the link is in a bad state. Before updating the site, solve the replication issue. If you need further assistance, contact Microsoft Support.<!-- 2838129 -->

#### File-based replication

For [file-based replication](../../plan-design/hierarchy/file-based-replication.md), check all inboxes for a backlog on both sending and receiving sites. If there are lots of stuck or pending replication jobs, wait until they clear out.<!-- SCCMDocs#1792 -->

- On the sending site, review **sender.log**.
- On the receiving site, review **despooler log**.

### Install all applicable critical Windows updates

Before you install an update for Configuration Manager, install any critical OS updates for each applicable site system. These servers include the site server, site database server, and remote site system roles. If an update that you install requires a restart, restart the applicable servers before you start the upgrade.

### Disable database replicas for management points at primary sites

Configuration Manager can't successfully update a primary site that has a database replica for management points enabled. Before you install an update for Configuration Manager, disable database replication.

For more information, see [Database replicas for management points](../deploy/configure/database-replicas-for-management-points.md).

### Set SQL Server Always On availability groups to manual failover

If you use an availability group, make sure that the availability group is set to manual failover before you start the update installation. After the site has updated, you can restore failover to be automatic. For more information, see [Prepare to use an availability group](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### Disable site maintenance tasks at each site

Before you install the update, disable any site maintenance task that might run during the time the update process is active. For example, but not limited to:

- Backup Site Server
- Delete Aged Client Operations
- Delete Aged Discovery Data

When a site database maintenance task runs during the update installation, the update installation can fail. Before you disable a task, record the schedule of the task so you can restore its configuration after the update has been installed.

For more information, see [Maintenance tasks](maintenance-tasks.md) and [Reference for maintenance tasks](reference-for-maintenance-tasks.md).

### Temporarily stop any antivirus software

Before you update a site, stop antivirus software on the Configuration Manager servers. The antivirus software can lock some files that need to be updated which causes our update to fail. <!--SMS.503481-->

### Create a backup of the site database

Before you update a site, back up the site database at the CAS and primary sites. This backup makes sure you have a successful backup to use for disaster recovery.

For more information, see [Backup and recovery](backup-and-recovery.md).

### Back up customized files

If you or a third-party product customizes any Configuration Manager configuration files, save a copy of your customizations.

For example, you add custom entries to the **osdinjection.xml** file in the `bin\X64` folder of your Configuration Manager installation directory. After you update Configuration Manager, these customizations don't persist. Reapply your customizations.

### Review hardware inventory customizations

<!-- 12613335 -->

If you changed the state of [hardware inventory classes in client settings](../../clients/manage/inventory/configure-hardware-inventory.md), when you update the site, some classes may revert to a default state. For example, if you disable the `SMS_Windows8Application` or `SMS_Windows8ApplicationUserInfo` classes, they're enabled after installing a Configuration Manager update.

When you customize hardware inventory classes, note their configuration before you install the update.

### Plan for client piloting

When you install a site update that also updates the client, test that new client update in pre-production before you update all production clients. To use this option, configure your site to support automatic upgrades for pre-production before beginning installation of the update.

For more information, see [Upgrade clients](../../clients/manage/upgrade/upgrade-clients.md) and [How to test client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md).

> [!NOTE]
> When you update to version 2107 or later, clients with PKI certificates will recreate self-signed certificates, but don't reregister with the site. Clients without a PKI certificate will reregister with the site, which can cause extra processing at the site. Make sure that your process to update clients allows for randomization. If you simultaneously update lots of clients, it may cause a backlog on the site server.

### Plan to use service windows

To define a period during which updates to a site server can be installed, use service windows. They can help you control when sites in your hierarchy install the update. For more information, see [Service windows for site servers](service-windows.md).

### Review supported extensions

<!--SCCMdocs#587-->
If you extend Configuration Manager with other products from Microsoft, Microsoft partners, or third-party vendors, confirm that those products support and are compatible with version 2403. Check with the product vendor for this information.

> [!TIP]
> If you develop a third-party add-on to Configuration Manager, you should test your add-on with every monthly [technical preview branch release](../../get-started/technical-preview.md). Regular testing helps confirm compatibility, and allows for early reporting of any issues with standard interfaces.

### Disable any custom solutions

If your site has any custom solutions based on the Configuration Manager SDK or PowerShell, disable this code before you update the site. Make sure to test this custom code in a lab environment to make sure it's compatible with the new version.

> [!NOTE]
> Starting in version 2111, third-party add-ons that use Microsoft .NET Framework and rely on Configuration Manager libraries also need to use .NET 4.6.2 or later. For more information, see [External dependencies require .NET 4.6.2](../../../develop/core/changes/whats-new-sdk.md#external-dependencies-require-net-462)<!--10529267-->.

### Read the release notes

Before you start the update, review the current release notes. With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a Microsoft Support article.

Feature-specific documentation may include information about known issues that affect core scenarios.

For more information, see the [Release notes](../deploy/install/release-notes.md).

## Install the update

### Run the setup prerequisite checker

When the console lists the update as **Available**, you can run the prerequisite checker before installing the update. (When you install the update on the site, prerequisite checker runs again.)

To run a prerequisite check from the console, go to the **Administration** workspace, and select **Updates and Servicing**. Select the **Configuration Manager 2403** update package, and select **Run prerequisite check** in the ribbon.

For more information, see the section to **Run the prerequisite checker before installing an update** in [Before you install an in-console update](prepare-in-console-updates.md#before-you-install-an-in-console-update).

> [!IMPORTANT]  
> When the prerequisite checker runs, the process updates some product source files that are used for site maintenance tasks. After running the prerequisite checker, but before installing the update, if you need to do a site maintenance task, run **Setupwpf.exe** (Configuration Manager Setup) from the CD.Latest folder on the site server.

### Update sites

You're now ready to start the update installation for your hierarchy. For more information about installing the update, see [Install in-console updates](install-in-console-updates.md).

You may plan to install the update outside of normal business hours. Determine when the process will have the least effect on your business operations. Installing the update and its actions reinstall site components and site system roles.

For more information, see [Updates for Configuration Manager](updates.md).

## Post-update checklist

After the site updates, use the following checklist to complete common tasks and configurations.

### Confirm version and restart (if necessary)

Make sure each site server and site system role is updated to version 2403. In the console, add the **Version** column to the **Sites** and **Distribution Points** nodes in the **Administration** workspace. When necessary, a site system role automatically reinstalls to update to the new version.

Consider restarting remote site systems that don't successfully update at first. Review your site infrastructure and make sure that applicable site servers and remote site system servers successfully restarted. Typically, site servers restart only when Configuration Manager installs .NET as a prerequisite for a site system role.

### Confirm site-to-site replication is active

In the Configuration Manager console, go to the following locations to view the status, and make sure that replication is active:  

- **Monitoring** workspace, **Site Hierarchy** node  

- **Monitoring** workspace, **Database Replication** node  

For more information, see the following articles:  

- [Monitor hierarchy and replication infrastructure](monitor-hierarchy.md)
- [About the Replication Link Analyzer](monitor-replication.md#BKMK_RLA)  

### Update Configuration Manager consoles

Update all remote Configuration Manager consoles to the same version. You're prompted to update the console when:  

- You open the console.  

- You go to a new node in the console.  

### Reconfigure database replicas for management points

After you update a primary site, reconfigure the database replica for management points that you uninstalled before you updated the site. For more information, see [Database replicas for management points](../deploy/configure/database-replicas-for-management-points.md).  

### Reconfigure availability groups

If you use an availability group, reset the failover configuration to automatic. For more information, see [Prepare to use an availability group](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).<!-- SCCMDocs #1366 -->

### Reconfigure any disabled maintenance tasks

If you disabled database [maintenance tasks](maintenance-tasks.md) at a site before installing the update, reconfigure those tasks. Use the same settings that were in place before the update.  

### Restore hardware inventory customizations

<!-- 12613335 -->

If you changed the state of [hardware inventory classes in client settings](../../clients/manage/inventory/configure-hardware-inventory.md), when you update the site, some classes may revert to a default state. For example, if you disable the `SMS_Windows8Application` or `SMS_Windows8ApplicationUserInfo` classes, they're enabled after installing a Configuration Manager update.

When you customize hardware inventory classes, review their configuration after you install the update to make sure they are configured as you intend.

<!-- ### Restore user state from active deployments-->

<!-- 10362100 -->

<!-- If you have any active user state migrations, before you update the Configuration Manager client on those devices, restore the user state. Due to [changes to the encryption algorithm in version 2103](../../plan-design/changes/whats-new-in-version-2103.md#encryption-algorithm-to-capture-and-restore-user-state), the updated client will fail to restore the user state when it tries to use a different encryption algorithm.-->

### Update clients

Update clients per the plan you created, especially if you configured client piloting before installing the update. For more information, see [How to upgrade clients for Windows computers](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

### Third-party extensions

If you use any extensions to Configuration Manager, update them to a version that supports and is compatible with Configuration Manager version 2403.

### Enable any custom solutions

Enable any custom solutions based on the Configuration Manager SDK or PowerShell that you've already tested in a lab environment with version 2403.

### Update boot images and media

<!--SCCMDocs issue 775-->

Use the **Update Distribution Points** action for any boot image that you use, whether it's a default or custom boot image. This action makes sure that clients can use the latest version. Even if there isn't a new version of the Windows ADK, the Configuration Manager client components may change with an update. If you don't update boot images and media, task sequence deployments may fail on devices.

When you update the site, Configuration Manager automatically updates the *default* boot images. It doesn't automatically distribute the updated content to distribution points. Use the **Update Distribution Points** action on specific boot images when you're ready to distribute this content across your network.

> [!NOTE]
> For default boot images, the site always uses the current version of the Configuration Manager client that matches the site's version.<!-- 11131898 --> Even if you configure automatic client upgrades to use a [pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md), that feature doesn't apply to boot images.<!-- 9616354 -->

After updating the site, manually update any *custom* boot images. This action updates the boot image with the latest client components if necessary, optionally reloads it with the current Windows PE version, and redistributes the content to the distribution points.

For more information, see [Update distribution points with the boot image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

### Update PowerShell help content

To get the latest information for the Configuration Manager PowerShell module, use the [Update-Help](/powershell/module/microsoft.powershell.core/update-help) cmdlet. Run this cmdlet on all computers with the Configuration Manager console. This help content is the same as what's published for the [ConfigurationManager module](/powershell/module/configurationmanager/).

For more information, see [Configuration Manager PowerShell cmdlets: Update help](/powershell/sccm/overview#update-help).

## Next steps

Review the [release notes](../deploy/install/release-notes.md). This article can be updated regularly, especially right after a new current branch release. You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../../../use-docs.md#notifications).
