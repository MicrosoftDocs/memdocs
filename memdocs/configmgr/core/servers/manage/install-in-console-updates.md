---
title: In-console updates
titleSuffix: Configuration Manager
description: Install updates to Configuration Manager from the Microsoft cloud
ms.date: 07/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
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

  - Prerequisite errors always stop the update installation. Fix errors before you can successfully retry the update installation. For more information, see [Retry installation of a failed update](#retry-installation-of-a-failed-update).

  - Prerequisite warnings can also stop the update installation. Fix warnings before you retry the update installation. For more information, see [Retry installation of a failed update](#retry-installation-of-a-failed-update).

  - **Ignore any prerequisite check warnings and install this update regardless of missing requirements**: Set a condition for the update installation to ignore prerequisite warnings. This option allows the update installation to continue. If you don't select this option, the update installation stops on a warning. Unless you've previously run the prerequisite check and fixed prerequisite warnings for a site, don't use this option.

    In both the **Administration** and **Monitoring** workspaces, the Updates and Servicing node includes a button on the ribbon named **Ignore prerequisite warnings**. This button becomes available when an update package fails to complete installation because of prerequisite check warnings. For example, you install an update without using the option to ignore prerequisite warnings (from within the Updates Wizard). The update installation stops with a state of prerequisite warning but no errors. Later, you select **Ignore prerequisite warnings** in the ribbon. This action triggers an automatic continuation of that update installation, which ignores prerequisite warnings. When you use this option, the update installation automatically continues after a few minutes.

- When an update applies to the Configuration Manager client, choose to test the client update with a limited set of clients. For more information, see [How to test client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md).

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

  - **Post Installation**: For more information, see [post installation tasks](#post-installation-tasks).

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

- Manually update secondary sites from within the Configuration Manager console. For more information, see [start the update installation at a secondary site](#bkmk_secondary).

- Until all sites in your hierarchy update to the new version, your hierarchy operates in a mixed version mode. For more information, see [Interoperability between different versions](../../plan-design/hierarchy/interoperability-between-different-versions.md).

### 5. Update Configuration Manager consoles

After a CAS or primary site updates, each Configuration Manager console that connects to the site must also update. You're prompted to update a console:

- When you open the console

- When you go to a new node in an open console

Update the console right away after the site updates.

After the console update completes, verify the console and site versions are correct. Go to **About Configuration Manager** at the top-left corner of the console.

> [!NOTE]
> The console version is slightly different from the site version. The minor version of the console corresponds to the Configuration Manager release version. For example, in Configuration Manager version 1802 the initial site version is 5.0.8634.1000, and the initial console version is 5.**1802**.1082.1700. The build (1082) and revision (1700) numbers may change with future hotfixes.

## Post-installation tasks

When a site installs an update, there are several tasks that can't start until after the update completes installation on the site server. This list includes the post-installation tasks that are critical for site and hierarchy operations. Because they're critical, they're actively monitored. Other tasks that aren't directly monitored include the reinstallation of site system roles. To view the status of the critical post-installation tasks, select the **Post Installation** task while monitoring the update installation for a site.

Not all tasks complete immediately. Some tasks don't start until each site completes installation of the update. New functionality you might expect can be delayed until these tasks complete. Turning on new features doesn't start until all sites complete update installation, so new features might not be visible for some time.

The post installation tasks include:

- **Installing SMS_EXECUTIVE service**

  - Critical service that runs on the site server.
  - Reinstallation of this service should complete quickly.

- **Installing SMS_DATABASE_NOTIFICATION_MONITOR component**

  - Critical site component thread of SMS_EXECUTIVE service.
  - Reinstallation of this service should complete quickly.

- **Installing SMS_HIERARCHY_MANAGER component**

  - Critical site component that runs on the site server.
  - Responsible for reinstalling roles on site system servers. Status for individual site system role reinstallation doesn't display.
  - Reinstallation of this service should complete quickly.

    > [!NOTE]
    > Some Configuration Manager site roles share the client framework. For example, the management point and pull distribution point. When these roles update, the client version on these servers updates at the same time. For more information, see [How to upgrade clients](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Installing SMS_REPLICATION_CONFIGURATION_MONITOR component**

  - Critical site component that runs on the site server.
  - Reinstallation of this service should complete quickly.

- **Installing SMS_POLICY_PROVIDER component**

  - Critical site component that runs only on primary sites.
  - Reinstallation of this service should complete quickly.

- **Monitoring replication initialization**

  - This task only displays at the CAS and child primary sites.
  - Dependent on the SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Should complete quickly.

- **Updating Configuration Manager Client Preproduction Package**

  - This task displays even when client preproduction (also called client piloting) isn't enabled for use.
  - Doesn't start until all sites in the hierarchy finish installing the update.

- **Updating Client folder on Site Server**

  - This task doesn't display if you use the client in preproduction.
  - Should complete quickly.

- **Updating Configuration Manager Client Package**

  - This task doesn't display if you use the client in preproduction.
  - Finishes only after all sites install the update.

- **Turning on Features**

  - This task displays only at the top-tier site of the hierarchy.
  - Doesn't start until all sites in the hierarchy finish installing the update.
  - Individual features aren't displayed.

## Retry installation of a failed update

When an update fails to install, review the in-console feedback to identify resolutions for warnings and errors. For more details, view the **ConfigMgrPrereq.log** on the site server. Before you retry the installation of an update, you must fix errors, and should fix warnings.

> [!TIP]
> If an update has problems downloading or replicating, use the [update reset tool](update-reset-tool.md).

When you're ready to retry the installation of an update, select the failed update, and then choose an applicable option. The update installation retry behavior depends on the node where you start the retry, and the retry option that you use.

### Retry installation for the hierarchy

Retry the installation of an update for the entire hierarchy when that update is in one of the following states:

- Prerequisite checks passed with one or more warnings, and the option to ignore prerequisite check warnings wasn't set in the Update Wizard. (The update's value for **Ignore Prereq Warning** in the **Updates and Servicing** node is **No**.)

- Prerequisite failed

- Installation failed

- Replication of the content to the site failed

Go to the **Administration** workspace and select the **Updates and Servicing** node. Select the update, and then choose one of the following options:

- **Retry**: When you **Retry** from **Updates and Servicing**, the update install starts again and automatically ignores prerequisite warnings. If content replication previously failed, content for the update replicates again.

- **Ignore prerequisite warnings**: If the update install stops because of a warning, you can then choose **Ignore prerequisite warnings**. This action allows the installation of the update to continue after a few minutes, and uses the option to ignore prerequisite warnings.

### Retry installation for the site

Retry the installation of an update at a specific site when that update is in one of the following states:

- Prerequisite checks passed with one or more warnings, and the option to ignore prerequisite check warnings wasn't set in the Update Wizard. (The updates value for **Ignore Prereq Warning** in the Updates and Servicing node is **No**.)

- Prerequisite failed

- Installation failed

Go to the **Monitoring** workspace, and select the **Site Servicing Status** node. Select the update, and then choose one of the following options:

- **Retry**: When you **Retry** from **Site Servicing Status**, you restart the installation of the update at only that site. Unlike running **Retry** from the **Updates and Servicing** node, this retry doesn't ignore prerequisite warnings.

- **Ignore prerequisite warnings**: If the update install stops because of a warning, you can then select **Ignore prerequisite warnings**. This action allows the installation of the update to continue after a few minutes, and uses the option to ignore prerequisite warnings.

## Report setup and upgrade failures to Microsoft
<!--5622909-->
Starting in Configuration Manager version 2010, if the setup or update process fails to complete successfully, you can report the error directly to Microsoft. If a failure occurs, the **Report update error to Microsoft** button is enabled. When you use the button, an interactive wizard opens allowing you to provide more information to us. When running [setup from the media](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md) rather than the console, you'll also be given the **Report update error to Microsoft** option if setup fails.

> [!IMPORTANT]
> For business-impacting issues, contact [Microsoft support](https://aka.ms/cmcbsupport) to open a new support request. Reporting setup and upgrade failures from the console is for providing product feedback on setup errors you may have encountered. Reporting an error doesn't generate a support request.

To report upgrade failures to Microsoft:

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Updates and Servicing**.

1. Select an update then select **Report update error to Microsoft** in the ribbon.

   :::image type="content" source="./media/5622909-report-error.png" alt-text="Report update error to Microsoft button in the ribbon." lightbox="./media/5622909-report-error.png":::

1. Before you submit the feedback, you'll be given options to:

   - Attach other files

   - Provide your email address if you're willing to be contacted about the error.

1. When you submit feedback, you'll be given a transaction ID for the feedback. A status message is also generated with this information.

   - Message ID 53900 is a successful submission.

   - Message ID 53901 is a failed submission.

## After a site installs an update

After the site updates, review the post-update checklist for the applicable version:

- [Post-update checklist for version 2107](checklist-for-installing-update-2107.md#post-update-checklist)

- [Post-update checklist for version 2103](checklist-for-installing-update-2103.md#post-update-checklist)

- [Post-update checklist for version 2010](checklist-for-installing-update-2010.md#post-update-checklist)

- [Post-update checklist for version 2006](checklist-for-installing-update-2006.md#post-update-checklist)

- [Post-update checklist for version 2002](checklist-for-installing-update-2002.md#post-update-checklist)

## Next steps

Some updates include optional features, which you can enable during or after installation.
> [!div class="nextstepaction"]
> [Optional features](optional-features.md)
