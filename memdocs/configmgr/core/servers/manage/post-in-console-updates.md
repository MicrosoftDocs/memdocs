---
title: After the site updates
titleSuffix: Configuration Manager
description: Learn what to do after the Configuration Manager site installs an in-console update.
ms.date: 01/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# After the site updates

*Applies to: Configuration Manager (current branch)*

After you [install an in-console update for Configuration Manager](install-in-console-updates.md), the site does additional processing in the background. There are also additional steps that you may need to take after the update is complete. If something goes wrong, use the steps below to help troubleshoot and retry the update.

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

- [Post-update checklist for version 2207](checklist-for-installing-update-2207.md#post-update-checklist)

- [Post-update checklist for version 2203](checklist-for-installing-update-2203.md#post-update-checklist)

- [Post-update checklist for version 2111](checklist-for-installing-update-2111.md#post-update-checklist)

- [Post-update checklist for version 2107](checklist-for-installing-update-2107.md#post-update-checklist)

- [Post-update checklist for version 2103](checklist-for-installing-update-2103.md#post-update-checklist)



## Next steps

Some updates include optional features, which you can enable during or after installation.
> [!div class="nextstepaction"]
> [Optional features](optional-features.md)
