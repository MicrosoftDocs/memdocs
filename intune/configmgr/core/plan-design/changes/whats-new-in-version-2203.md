---
title: What's new in version 2203
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2203 of Configuration Manager current branch.
ms.date: 04/26/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart
---

# What's new in version 2203 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2203 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2010 or later. <!-- baseline only statement:--> When installing a new site, this version of Configuration Manager will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability of the in-console update. This article summarizes the changes and new features in Configuration Manager, version 2203.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2203](../../servers/manage/checklist-for-installing-update-2203.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2203.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Cloud-attached management

### Prefer cloud-based software update points
<!--7759984-->
Clients now prefer to scan against a cloud management gateway (CMG) software update point (SUP) over an on-premises SUP when the boundary group uses the **Prefer cloud based source over on-premises source** option. To reduce the performance effect of this change, existing clients don't automatically switch to a cloud-based software update point.

For more information, see [Boundary groups and software update points](../../servers/deploy/configure/boundary-groups-software-update-points.md#bkmk_prefer_cmgsup).

## Site infrastructure

### Visualize content distribution status

<!--9495651-->

You can now monitor content distribution path and status in a graphical format. The graph shows distribution point type, distribution state, and associated status messages. This visualization allows you to more easily understand the status of your content package distribution. It helps you answer questions like:

- Has the site successfully distributed the content?
- Is the content distribution in progress?
- Which distribution points have already processed the content?

:::image type="content" source="media/9495651-view-content-distribution-small.png" alt-text="Visualization of content distribution status of the Configuration Manager client package in an example hierarchy.":::

For more information, see [Visualize content distribution status](../../servers/deploy/configure/visualize-content-distribution-status.md).

### Improvements to Power BI Report Server integration
<!--12487076-->
We've made the following improvements for Power BI Report Server integration:

- You can now use Microsoft Power BI Desktop (Optimized for Power BI Report Server) versions that were released after January 2021
- Configuration Manager now correctly handles Power BI reports saved by Power BI Desktop (optimized for Power BI Report Server) May 2021 or later.

For more information, see [Integrate with Power BI Report Server](../../servers/manage/powerbi-report-server.md).

### Exclude data warehouse reporting tables from synchronization
<!--12441118-->
When you install the [data warehouse](../../servers/manage/data-warehouse.md), it synchronizes a set of default tables from the site database. These tables are required for data warehouse reports. While troubleshooting issues, you may want to stop synchronizing these default tables. Starting in this release, you can exclude one or more of these required tables from synchronization.

For more information, see [Exclude data warehouse reporting tables from synchronization](../../servers/manage/data-warehouse.md#bkmk_exclude).

### Improvements to management insights

The following improvements have been made to management insights:

- A new management insights group was added to **Management Insights**. The **Deprecated and unsupported features** group contains rules that will help you manage and remove deprecated features. The prerequisite checker will also check for deprecated and unsupported features during site installs and upgrades. <!--10875436, 12451634 -->

- A new rule for detecting Windows Server 2012 and 2012 R2 was added to the **Proactive Maintenance** group. <!--9519162-->

For more information, see [Management insights for deprecated and unsupported features](../../servers/manage/management-insights.md#deprecated-and-unsupported-features) and [Management insights for proactive maintenance](../../servers/manage/management-insights.md#proactive-maintenance).

## Client management

### Deployment Status client notification actions
<!--7079837-->
You can now perform client notification actions, including **Run Scripts**, from the **Deployment Status** view.

For more information, see [Review deployment details](../../../apps/deploy-use/monitor-applications-from-the-console.md#review-deployment-details).

## Collections

### Delete collection references

<!--9708999-->

Previously, when you would delete a collection with dependent collections, you first had to delete the dependencies. The process of finding and deleting all of these collections could be difficult and time consuming. Now when you delete a collection, you can review and delete its dependent collections at the same time.

For more information, see [Delete collection references](../../clients/manage/collections/manage-collections.md#delete-collection-references).

<!-- ## Software Center -->

## Software updates

### LEDBAT support for software update points
<!--4639895-->
You can now enable Windows Low Extra Delay Background Transport (LEDBAT) for your software update points. LEDBAT adjusts download speeds during client scans against WSUS to help control network congestion.

For more information, see [Install a software update point](../../../sum/get-started/install-a-software-update-point.md#bkmk_ledbat).

### Pre-download content for available software updates
<!--4497776-->
You can now pre-download content for software updates that are included in available deployments. Required deployments already pre-download content by default. Enabling this new setting reduces installation wait times for clients since installation notifications won't be visible in Software Center until the content has fully downloaded.

For more information, see [Deploy software updates](../../../sum/deploy-use/manually-deploy-software-updates.md#process-to-manually-deploy-the-software-updates-in-a-software-update-group).

### Customize maximum run time for other software update types
<!--12770887-->
Previously, software updates that didn't belong to the following update categories defaulted to a maximum run time of 60 minutes (or 10 minutes prior to version 2103):
- Windows feature updates
- Windows non-feature updates
- Office 365 updates

You can now customize the maximum run time for all other software updates, which includes third-party updates.

For more information, see [Maximum run time](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime) and [Install and configure a software update point](../../../sum/get-started/install-a-software-update-point.md#bkmk_maxruntime).

### ADR scheduling improvements for deployments
<!--12707738, 7033417-->
The **Software available time** and **Installation deadline** for deployments created by an automatic deployment rule (ADR) are now calculated based on the time the ADR evaluation is scheduled and starts. Previously, these times were calculated based on when the ADR evaluation completed. This change makes the  **Software available time** and **Installation deadline** consistent and predictable for deployments.

For more information, see [Automatic deployment rules (ADR)](../../../sum/deploy-use/automatically-deploy-software-updates.md).

### Added folder support for nodes in the Software Library
<!--3601129-->

You can now organize software update groups and packages by using folders. This change allows for better categorization and management of software updates.

For more information, see [Deploy software updates](../../../sum/deploy-use/deploy-software-updates.md#bkmk_folder).

### Alerts for orchestration groups
<!--12725116-->
If an orchestration group fails, an alert is now displayed in in **Monitoring** > **Alerts** > **Active Alerts**. For more information, see [Monitor orchestration groups](../../../sum/deploy-use/monitor-orchestration-groups.md#bkmk_alerts).

## OS deployment

### Escrow BitLocker recovery password to the site during a task sequence

<!--10454717-->

You can now configure the **Enable BitLocker** step of a task sequence to escrow the BitLocker recovery information for the OS volume to Configuration Manager. Previously, you had to escrow to Active Directory, or wait for the Configuration Manager client to receive BitLocker management policy after the task sequence. This new option makes sure that the device is fully protected by BitLocker when the task sequence completes, and that you can recover the OS volume immediately.

For more information, see [Task sequence steps: Enable BitLocker](../../../osd/understand/task-sequence-steps.md#enable-bitlocker).

### Custom icon support for task sequences and packages

<!--12486335-->

Previously, task sequences and legacy packages would always display a default icon in Software Center. Based on your feedback, you can now add custom icons for task sequences and legacy packages. These icons appear in Software Center when you deploy these objects. Instead of a default icon, a custom icon can improve the user experience to better identify the software.

For more information, see [Manage task sequences](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#more-options-tab) and [Packages and programs](../../../apps/deploy-use/packages-and-programs.md#custom-icons-for-packages).

<!--## Protection-->

## Application management

### Improvements to implicit uninstall
<!--12488148-->

If you deploy an application or app group to a user collection that's based on a security group, and you enable implicit uninstall, changes to the security group are now honored. When the site discovers the change in group membership, Configuration Manager uninstalls the app for the user that you removed from the security group.

For more information, see [implicit uninstall](../../../apps/deploy-use/uninstall-applications.md#implicit-uninstall).

## Community hub

### Delete a contribution you made to Community hub
<!--10416767-->
You can now delete contributions you've made to the Community hub. For more information, see [Contribute to Community hub](../../servers/manage/community-hub-contribute.md#bkmk_delete).

### Search filter list
<!--7281922-->
The console now displays a list of filters you can use when searching the Community hub. For more information, see [Filter Community hub content when searching](../../servers/manage/community-hub.md#bkmk_search).

## Configuration Manager console

### Dark theme for the console
<!--9070525-->
The Configuration Manager console now offers a dark theme. For more information, see [How to use the Configuration Manager console](../../servers/manage/admin-console.md#bkmk_dark).

### Improvements for sending feedback
<!--11754191, 12890088-->
- You now have the ability to connect feedback you send to Microsoft through the Configuration Manager console to an authenticated Azure Active Directory (Azure AD) user account or Microsoft Account (MSA). User authentication will help Microsoft ensure the privacy of your feedback and diagnostic data.
- The feedback button is now displayed in other console locations.

For more information, see [Product feedback](../../understand/product-feedback.md#recent-changes-to-feedback).

### Improvements to dashboards
<!--10024154-->
Dashboards, such as the **Windows Servicing** and **Microsoft Edge Management** dashboards, now use the Microsoft Edge WebView2 Runtime. To use dashboards, install the WebView2 console extension, then reopen the console.

For more information, see the [WebView2 console extension](../../servers/manage/admin-console-extensions.md#bkmk_notification).

### Console and user experience improvements
<!--12726153-->
Based on your feedback, we've made a few improvements to the console and user experience.

- When using temporary device nodes, device actions like **Run Scripts** are now available to make the experience in the console consistent.
- Other management insights rules now have drill-through actions.
- Copy/paste is available for more objects from details panes.
- The **Name** property is added to the details pane for configuration items, configuration item related policies, and applications.
- Software update search results and the search criteria are now cached when you navigate to another node. When you navigate back to the **All Software Updates** node, your search criteria and results are preserved from your last query.
- Added a search filter to the **Products** and **Classifications** tabs in the **Software Update Point Component Properties** <!--10998089, 9575773-->
- You can now exclude subcontainers when doing **Active Directory System Discovery** and **Active Directory User Discovery** in untrusted domains <!--4655840, 9575773-->
- Added a **Cloud Sync** column to collections to indicate if the collection is synchronizing with Azure Active Directory <!--12433024, 9575773-->
- Added the **Collection ID** to the collection summary details tab <!--12630582, 9575773-->
- Increased the size of the **Membership Rules** pane in the **Properties** page for collections <!--12947295, 9575773 -->
- Added a **View Script** option for **Run PowerShell Script** steps when using the **View** action for a task sequence <!--12498818, 9575773 -->

For more information, see [Console changes and tips](../../servers/manage/admin-console-tips.md#bkmk_2203).

<!--## Tools-->

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

The following features are deprecated. You can still use them now, but Microsoft plans to end support in the future.

- The Configuration Manager client for **macOS** and Mac client management. For more information, see [Supported clients: Mac computers](../configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)
- The site system roles for on-premises MDM and macOS clients: **enrollment proxy point and enrollment point**

As previously announced, version 2203 drops support for the following features:

- The ability to deploy a cloud management gateway (CMG) as a **cloud service (classic)**. All CMG deployments should use a [virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets).<!--10966586,13235079-->

- The following compliance settings for **Company resource access**: <!-- 9315387 -->
  - Certificate profiles and the certificate registration point site system role
  - VPN profiles
  - Wi-Fi profiles
  - Windows Hello for Business settings
  - Email profiles
  - Co-management resource access workload

    For more information, see [Frequently asked questions about resource access deprecation](../../../protect/plan-design/resource-access-deprecation-faq.yml).

## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

- [Task sequence debugger](../../../osd/deploy-use/debug-task-sequence.md)

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2203 release notes](/powershell/sccm/2203-release-notes).

Aside from new features, this release also includes other changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2203](../../../hotfix/2203/13174460.md).

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

<!--
At this time, version 2203 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2203.md#early-update-ring).
-->

As of April 26, 2022, version 2203 is globally available for all customers to install.-->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2203](../../servers/manage/checklist-for-installing-update-2203.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2203.md#post-update-checklist).
