---
title: What's new in version 2111
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2111 of Configuration Manager current branch.
ms.date: 11/19/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# What's new in version 2111 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2111 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2006 or later. <!-- baseline only statement: When installing a new site, it will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability.--> This article summarizes the changes and new features in Configuration Manager, version 2111.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2111](../../servers/manage/checklist-for-installing-update-2111.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2111.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2111+-+Configuration+Manager%22&locale=en-us`

## Cloud-attached management

### Simplified cloud attach configuration

<!--10964629-->

We've simplified the process to cloud attach your Configuration Manager environment. You can now choose to use a streamlined set of recommended defaults when cloud attaching your environment. By using the recommended default settings, your eligible devices will be cloud attached and you'll enable capabilities like rich analytics, cloud console, and real-time device querying.

<!-- For more information, see ... -->

## Site infrastructure

### Improvements to external notifications

<!--10615989-->

Starting in Configuration Manager current branch version 2107, you could enable the site to send notifications to an external system or application. This feature used a PowerShell script to manage the status filter rules and subscriptions.

This release adds support in the Configuration Manager console to create or edit a subscription for external notifications. It supports events for status filter rules and application approval requests.

<!-- For more information, see [External notifications](../../servers/manage/external-notifications.md). -->

### .NET version 4.6.2 prerequisite check is an error

<!--10644702-->

Configuration Manager current branch version 2107 has a warning prerequisite rule that checks for Microsoft .NET Framework version 4.6.2. This version of .NET is required on site servers, specific site systems, clients, and the Configuration Manager console.

Starting in this release, this prerequisite rule for .NET 4.6.2 is an error. Until you upgrade .NET, you can't continue installing or updating the site to this version of Configuration Manager.

<!-- For more information, see [List of prerequisite checks for Configuration Manager](../../servers/deploy/install/list-of-prerequisite-checks.md#required-version-of-microsoft-net-framework). -->

### Improvements to VPN boundary types

<!--7822886-->

If you use the **VPN** boundary type, you can now match the start of a connection name or description instead of the whole string. Some third-party VPN drivers dynamically create the connection, which starts with a consistent string but also has a unique connection identifier. For example, `Virtual network adapter #19`. When you use the **Connection name** or **Connection description** options, also use the new **Starts with** option.

<!-- For more information, see [Define network locations as boundaries for Configuration Manager](../../servers/deploy/configure/boundaries.md#vpn). -->

### Status messages for console extensions

<!--11048976-->

To improve the visibility and transparency of console extensions, the site now creates status messages for related events. These status messages have IDs from **54201** to **54208**.

<!-- For more information, see ... -->

## Client management

### Improvements to client health dashboard

<!--5728069-->

This release includes improvements to the **Client health dashboard**.

<!-- For more information, see [Client health dashboard](../../clients/manage/monitor-clients.md#bkmk_health). -->

## Software Center

### Software Center notifications display with logo

<!--4993167-->

If you enable Software Center customizations, then notifications on Windows 10 devices display the logo that you configure in client settings. This change helps users to trust these notifications.

<!-- When you deploy software to a client, the user sees notifications with your logo. The following example uses a star logo:

media/4993167-notification-with-logo.png
:::image type="content" source="" alt-text="New software is available notification with custom logo":::

For more information about customizing Software Center, see [About client settings: Software Center](../../clients/deploy/about-client-settings.md#software-center).
 -->

## Application management

### Implicit uninstall for user collections

<!--10393847-->

In Configuration Manager current branch version 2107, you can enable an application deployment to support.

Starting in this release, this behavior also applies to deployments to user collections. If a user is in a collection, the application installs. Then when you remove the user from the collection, the application uninstalls.

<!-- For more information, see [implicit uninstall](../../../apps/deploy-use/uninstall-applications.md#implicit-uninstall). -->

### Improvements to application groups

This release includes the following improvements to application groups:

- Now when you deploy an app group as required to a device or user collection, you can specify that it automatically uninstalls when the resource is removed from the collection.<!--10479618-->

- The following app approval behaviors are now supported with app groups:<!-- 10992210 -->

<!-- For more information, see [Create application groups](../../../apps/deploy-use/create-app-groups.md). -->

## OS deployment

### Task sequence check for TPM 2.0

<!--9575077-->

To help you better deploy Windows 11, the **Check Readiness** step in the task sequence now includes checks for TPM 2.0.

<!-- For more information, see [Task sequence steps: Check Readiness](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness). -->

### Improvements to the Windows servicing dashboard

<!--10579996-->
We now display a **Windows 11 Latest Feature Updates** chart in the **Windows Servicing** dashboard. The new chart makes it easier to determine how many of your Windows 11 clients are on the latest feature update. To display the dashboard, go to **Software Library** > **Overview** > **Windows Servicing**.

For more information, see [The Windows servicing dashboard](../../../osd/deploy-use/manage-windows-as-a-service.md#bkmk_2103-dashboard).

## Protection


## Software updates

### Improvements to ADR search criteria

<!--7033309-->

This release adds more options to the **Date Released or Revised** search criteria for automatic deployment rules.

<!-- For more information, see [Automatically deploy software updates](../../../sum/deploy-use/automatically-deploy-software-updates.md). -->

### Approvals for orchestration group scripts

<!--9957939-->

Pre and post-scripts for orchestration groups now require approval to take effect. If you open, author, or modify a script, approval for the script is required from another admin. When selecting an approved script from the **Scripts** library, no additional approval is needed. To assist you with script approval, the following two tabs were added to the details pane for **Orchestration Groups**:

- **Summary**: Contains information about the selected orchestration group, including the **Approval State** of scripts.
- **Scripts**: Lists information about pre and post-scripts, including the timeout, approver, and approval state for each script.

<!-- For more information, see [Orchestration groups in Configuration Manager](../../../sum/deploy-use/orchestration-groups.md). -->

### Enable update notifications from Microsoft 365 Apps

<!--10628998-->

You can now configure the end-user experience for Microsoft 365 Apps updates. This client setting allows you to enable or disable notifications from Microsoft 365 Apps for these updates. The new **Enable update notifications from Microsoft 365 Apps** option has been added to the **Software Updates** group of client settings.

<!-- For more information, see [About client settings in Configuration Manager](../../clients/deploy/about-client-settings.md). -->

## Configuration Manager console

### Custom properties for devices in the console

<!--10642650-->

In Configuration Manager current branch version 2107, you can use the administration service to set custom properties on devices. These custom properties let you add external data to a device to help with deployment targeting, collection building, and reporting.

Starting in this release, you can create and edit these custom properties in the Configuration Manager console. This new user interface makes it easier to view and edit these properties. You can still use the administration service interface to automate the process from an external system.

<!-- For more information, see [Custom properties for devices](../../../develop/adminservice/custom-properties.md). -->

### Export to CSV

<!--9663857-->

You can now export the contents of a grid view in the console along with the column headers to a comma-separated values (CSV) file that can be used to import to Excel or other applications. While you could previously cut and paste from a grid view, exporting to CSV makes extracting a large number of rows faster and easier.

<!-- For more information, see ... -->

### Import console extensions wizard

<!--9741121, 9761129-->

There's a new wizard for importing console extensions that are managed for the hierarchy. You no longer need to use a PowerShell script to import a signed or unsigned console extension.

<!-- For more information, see [Manage Configuration Manager console extensions](../../servers/manage/admin-console-extensions.md). -->

### Require installation of a console extension

<!--10486584-->

You can now require a console extension to be installed before it connects to the site. After you require an extension, it automatically installs for the local console the next time an admin launches it.

For more information, see [Manage Configuration Manager console extensions](../../servers/manage/admin-console-extensions.md).

### Send product feedback from wizard and property dialogs

<!--2711343-->

Wizards and some property pages now include an icon to provide feedback. When you select the feedback icon, the **Send a smile** and **Send a frown** options are displayed in the drop-down menu. The additional feedback locations allow you to quickly send feedback right from your current activity. The feedback icon in the admin console's ribbon has also been updated to the new icon.

<!-- For more information, see [Product feedback for Configuration Manager](../../understand/product-feedback.md). -->

### Console improvements
<!--9575773-->
In this release we've made the following improvements to the Configuration Manager console:

- Independent Software Vendors (ISVs) can create applications that extend Configuration Manager. They can use Configuration Manager to assign a certificate to an ISV proxy, which enables custom communication with the management point. To simplify the management of these ISV proxy certificates, you can now copy its GUID in the Configuration Manager console. <!-- For more information, see ... --><!--2842082-->

- When you show the members of a device collection, and select a device in the list, switch to the **Collections** tab in the details pane. This new view shows the list of collections of which the selected device is a member. It makes it easier for you to see this information.<!-- 10480635 -->

- When viewing a collection, you could previously see the amount of time the site took to evaluate the collection membership. This data is now also available in the **Monitoring** workspace.<!-- 9648622 --> When you select a collection in either subnode of the **Collection Evaluation** node, the details pane displays this collection evaluation time data.

For more information about improvements to the console, see [Configuration Manager console changes and tips](../../servers/manage/admin-console-tips.md).

## Tools

### Options for Support Center Data Collector and Client Tools

<!--9947307-->

The following new command-line options have been added to the Support Center Data Collector and Client Tools:

<!-- For more information, see [Support Center](../../support/support-center.md). -->

### Improvements to Support Center Log File Viewer and OneTrace

<!--9348231, 10915091-->

The Support Center **Log File Viewer** and **OneTrace** now display status messages in an easy to read format. Entries starting with `>>` are status messages that are automatically converted into a readable format when a log is opened. Search or filter on the `>>` string to find status messages in the log.

<!-- For more information, see [Support Center log file viewer](../../support/support-center.md#support-center-log-file-viewer) and [Support Center OneTrace](../../support/support-center-onetrace.md). -->

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

- The ability to deploy a cloud management gateway (CMG) as a **cloud service (classic)** is deprecated. All CMG deployments should use a [virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets).<!--10966586-->

As [previously announced](deprecated/removed-and-deprecated-cmfeatures.md), version 2111 drops support for the following features:

- Third-party add-ons that use Microsoft .NET Framework version 4.6.1 or earlier, and rely on Configuration Manager libraries. Such add-ons need to use .NET 4.6.2 or later. For more information, see [External dependencies require .NET 4.6.2](../../get-started/2021/technical-preview-2109.md#bkmk_dotnetsdk)<!--10529267-->.<!-- NEED FINAL LINK NOT TECH PREVIEW -->

## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):
<!-- UPDATE NEEDED -->
- [Cloud management gateway (CMG) with virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets) <!--3601040,8959690-->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2111 release notes](/powershell/sccm/2111-release-notes).

Aside from new features, this release also includes other changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2111].<!-- NEED FINAL LINK -->

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).
-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [9833643](../../../hotfix/2111/9833643.md) | Console update for Microsoft Endpoint Configuration Manager version 2111 | May 11, 2021 | No |
-->

## Next steps

At this time, version 2111 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2111.md#early-update-ring).

<!-- As of August 23, 2021, version 2111 is globally available for all customers to install. -->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2111](../../servers/manage/checklist-for-installing-update-2111.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2111.md#post-update-checklist).
