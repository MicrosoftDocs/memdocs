---
title: In-console updates
titleSuffix: Configuration Manager
description: Install updates to Configuration Manager from the Microsoft cloud.
ms.date: 12/04/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: Baladelli
ms.author: Baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Install in-console updates for Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article describes how to install updates from within the Configuration Manager console. Before you start, make sure to [Prepare to install in-console updates](prepare-in-console-updates.md).

When you're ready to install updates from within the Configuration Manager console, begin with the top-level site of your hierarchy. This site is either the central administration site (CAS) or a standalone primary site.

Install the update outside of normal business hours for each site to minimize the effect on business operations. The update installation might include actions like reinstalling site components and site system roles.

- Child primary sites automatically start the update after the CAS completes installation of the update. This process is by default and recommended. To control when a primary site installs updates, use [Service windows for site servers](service-windows.md).

- After the primary parent site update is complete, manually update secondary sites from within the Configuration Manager console. Automatic update of secondary site servers isn't supported.

- When you use a Configuration Manager console after the site is updated, you're prompted to update the console.

- After the site server successfully completes installation of an update, it automatically updates all applicable site system roles. However, all distribution points don't reinstall and go offline to update at the same time. Instead, the site server uses the site's content distribution settings to distribute the update to a subset of distribution points at a time. The result is that only some distribution points go offline to install the update. Distribution points that haven't begun to update or that have completed the update remain online and able to provide content to clients.

## Start the install

At the top-level site of your hierarchy, in the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. Select an update with the state of **Available**, and then choose **Install Update Pack** in the ribbon.

> [!NOTE]
> Your user account requires permissions to install updates. For more information, see [Permissions for in-console updates](prepare-in-console-updates.md#permissions).

### Start the update installation at a secondary site

After the parent primary site updates, update the secondary site from within the Configuration Manager console.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the secondary site you want to update, and then choose **Upgrade** in the ribbon.

1. Select **Yes** to start the update of the secondary site.

To monitor the update installation on a secondary site, select the secondary site, and choose **Show Install Status** in the ribbon. Also add the **Version** column to the Sites node so that you can view the version of each secondary site.

The status in the console may not refresh or it might show that the update failed. After a secondary site successfully updates, use the **Retry installation** option. This option doesn't reinstall the update for a secondary site that successfully installed the update, but forces the console to update the status.

## Install process

### 1. When the update installation starts

You're presented with the Updates Wizard that displays a list of the product areas that the update applies to.

- On the **General** page of the wizard, configure **Prerequisite warnings** as necessary:

  - Prerequisite errors always stop the update installation. Fix errors before you can successfully retry the update installation. For more information, see [Retry installation of a failed update](post-in-console-updates.md#retry-installation-of-a-failed-update).

  - Prerequisite warnings can also stop the update installation. Fix warnings before you retry the update installation. For more information, see [Retry installation of a failed update](post-in-console-updates.md#retry-installation-of-a-failed-update).

  - **Ignore any prerequisite check warnings and install this update regardless of missing requirements**: Set a condition for the update installation to ignore prerequisite warnings. This option allows the update installation to continue. If you don't select this option, the update installation stops on a warning. Unless you've previously run the prerequisite check and fixed prerequisite warnings for a site, don't use this option.

    In both the **Administration** and **Monitoring** workspaces, the Updates and Servicing node includes a button on the ribbon named **Ignore prerequisite warnings**. This button becomes available when an update package fails to complete installation because of prerequisite check warnings. For example, you install an update without using the option to ignore prerequisite warnings (from within the Updates Wizard). The update installation stops with a state of prerequisite warning but no errors. Later, you select **Ignore prerequisite warnings** in the ribbon. This action triggers an automatic continuation of that update installation, which ignores prerequisite warnings. When you use this option, the update installation automatically continues after a few minutes.

- When an update applies to the Configuration Manager client, choose to test the client update with a limited set of clients. For more information, see [How to test client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md).

- Starting in Configuration Manager 2107, sites that aren't already onboarded to Microsoft Endpoint Manager will be prompted to optionally cloud attach as part of the upgrade wizard. Environments are considered cloud attached if at least one of the following features are already enabled:

   - [Tenant attach](../../../tenant-attach/device-sync-actions.md)
   - [Co-management](../../../comanage/overview.md)
   - [Endpoint analytics](../../../../analytics/enroll-configmgr.md)

  If you don't wish to onboard, clear both of the **Enable Microsoft Intune admin center** and **Enable automatic client enrollment for co-management** options. <!--1074186-->

### 2. During the update installation

As part of the update installation, Configuration Manager does the following actions:

- Reinstalls any affected components, like site system roles or the Configuration Manager console.

- Manages updates to clients based on the selections that you made for client piloting, and for [automatic client upgrades](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

- Site system servers generally don't need to restart as part of the update. If a role uses .NET, and the package updates that prerequisite component, then the site system may restart. For more information, see [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md#net-version-requirements).

> [!TIP]
> When you install Configuration Manager updates, the site also updates the CD.Latest folder. For more information, see [The CD.Latest folder](the-cd.latest-folder.md).

### 3. Monitor the progress of updates as they install

Use the following steps to monitor progress:

- In the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. This node shows the installation status for all update packages.

- In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Updates and Servicing Status** node. This node shows the installation status of only the current update package that the site is installing.

    The update installation is divided into several phases for easier monitoring. For each of the following phases, more details in the installation status include which log file to view for more information:

  - **Download**: This phase applies only to the top-level site with the service connection point.

  - **Replication**

  - **Prerequisites Check**

  - **Installation**

  - **Post Installation**: For more information, see [post installation tasks](post-in-console-updates.md#post-installation-tasks).

- View the **CMUpdate.log** file in `<ConfigMgr_Installation_Directory>\Logs` on the site server.

>[!NOTE]
> During the **Installation** phase, you can see the state of the **Upgrade ConfigMgr database** task.
>
> - If the database upgrade is blocked, then you'll be given the warning **In progress, needs attention**.
>   - The cmupdate.log will log the program name and sessionid from SQL Server that is blocking the database upgrade.
> - When the database upgrade is no longer blocked, the status will be reset to **In progress** or **Complete**.
>   - When the database upgrade is blocked, a check is done every 5 minutes to see if it's still blocked.

### 4. When the update installation completes

After the first site update completes installation:

- Child primary sites install the update automatically. No further action is required.

- Manually update secondary sites from within the Configuration Manager console. For more information, see [start the update installation at a secondary site](#start-the-update-installation-at-a-secondary-site).

- Until all sites in your hierarchy update to the new version, your hierarchy operates in a mixed version mode. For more information, see [Interoperability between different versions](../../plan-design/hierarchy/interoperability-between-different-versions.md).

### 5. Update Configuration Manager consoles

After a CAS or primary site updates, each Configuration Manager console that connects to the site must also update. You're prompted to update a console:

- When you open the console

- When you go to a new node in an open console

Update the console right away after the site updates.

After the console update completes, verify the console and site versions are correct. Go to **About Configuration Manager** at the top-left corner of the console.

> [!NOTE]
> The console version is slightly different from the site version. The minor version of the console corresponds to the Configuration Manager release version. For example, in Configuration Manager version 2303 the initial site version is 5.0.9122.1000, and the initial console version is 5.**9122**.1082.1700. The build (1082) and revision (1700) numbers may change with future hotfixes.

## Next steps

Continue reading about what happens after the site updates, or what to do if the update fails.
> [!div class="nextstepaction"]
> [After the site updates](post-in-console-updates.md)
