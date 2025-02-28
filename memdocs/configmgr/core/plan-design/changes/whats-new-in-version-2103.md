---
title: What's new in version 2103
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2103 of Configuration Manager current branch.
ms.date: 06/11/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2103 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2103 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1910 or later. <!-- baseline only statement:--> When installing a new site, it will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability. This article summarizes the changes and new features in Configuration Manager, version 2103.

> [!NOTE]
> To better align with other releases within Microsoft Endpoint Manager, starting this year the current branch version names will be 2103, 2107, and 2111. They will still release every four months, and release at the same time of the year.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2103](../../servers/manage/checklist-for-installing-update-2103.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2103.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Microsoft Intune tenant attach

### Display all applications for a device in Microsoft Intune admin center
<!--8795301-->
The **Applications** view for a tenant attached device in Microsoft Intune admin center now displays more applications from Configuration Manager. Displayed applications include applications that are:
- Deployed to the device
- Deployed to a user that's logged in to the device, primary user of the device, and applications previously installed for the user

The option, **An administrator must approve a request for this application on the device**, is no longer required to be set on the device available deployment for applications to be listed in the admin center. This improvement allows you to review when application installations are expected to occur on a device.

For more information, see [Tenant attach: Install an application from the admin center](../../../tenant-attach/applications.md#bkmk_all).

### Antivirus policy exclusions merge
<!--9089764-->
When a tenant attached device is targeted with two or more antivirus policies, the settings for antivirus exclusions will merge before being applied to the client. This change results in the client receiving the exclusions defined in each policy, allowing for more granular control of antivirus exclusions.

For more information, see [antivirus policies](../../../tenant-attach/deploy-antivirus-policy.md#bkmk_exclusion).

### User discovery prerequisite simplification
<!--8126836 -->
The discovery prerequisite for user accounts accessing tenant attach features within **Microsoft Intune admin center** was simplified. The hybrid identity needs to be discovered by one of the following discovery methods instead of both:
- Azure Active Directory user discovery
- Active Directory user discovery

For more information, see [Tenant attach prerequisites](../../../tenant-attach/prerequisites.md).

### Application details
<!--8364465-->
When tenant attach is enabled, the applications pane in the Microsoft Intune admin center will show an **Error Description** if the application status is **Failed**.

For more information on the error code and troubleshooting steps, see [Application installation common error codes reference](../../../tenant-attach/app-install-error-reference.md).

<!-- 
## Cloud-attached management

## Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).
 -->

## Site infrastructure

### New prerequisite checks

When you install or update to version 2103, there are several new warning [prerequisite checks](../../servers/deploy/install/list-of-prerequisite-checks.md).

#### Enable the site for HTTPS-only or enhanced HTTP

<!-- 9390933,9572265 -->

If your site is configured to allow HTTP communication without enhanced HTTP, you'll see this warning. To improve the security of client communications, in the future Configuration Manager will require HTTPS communication or enhanced HTTP. Plan to configure the site for **HTTPS only** or to **Use Configuration Manager-generated certificates for HTTP site systems**. For more information, see the description of this [prerequisite check](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).

#### Deprecated Azure Monitor connector

<!--8269855-->

We continue to see broad adoption of native Azure Monitor log query groups as customers shift more of their workloads to the cloud. Because of this reason, starting in November 2020, the Configuration Manager feature to synchronize collections to Azure Monitor was deprecated.

When you update to this release, this check warns about the presence of the [Log Analytics connector for Azure Monitor](/azure/azure-monitor/platform/collect-sccm?context=%2fmem%2fconfigmgr%2fcore%2fcontext%2fcore-context). (This feature is called the *OMS Connector* in the Azure Services wizard.) This connector is deprecated, and will be removed from the product in a future release. At that time, this check will be an error that blocks upgrade.

#### SQL Server Express version

<!-- 9421748 -->

If you have a secondary site that uses SQL Server Express edition, this check warns if the version is earlier than SQL Server 2016 with service pack 2 (13.0.5026.0).

Microsoft recommends that you keep SQL Server Express up to date. For more information, see [Security for site administration](../hierarchy/security-and-privacy-for-site-administration.md#update-sql-server-express-at-secondary-sites).

<!-- 
## Client management
 -->

### Allow exclusion of organizational units (OU) from Active Directory User Discovery
<!--5193509-->

You can now exclude OUs from [Active Directory User Discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adud).

## Collections

### Improvements to the collection relationships viewer

<!--8543508-->

Starting in version 2010, you can view dependency relationships between collections in a graphical format. The relationships for a collection were presented as two hierarchical trees, one for dependents and the other for dependencies. In this release, you can view both parent and child relationships together in a single graph. This change allows you to quickly see an overview of all the relationships of a collection at once and then drill down into specific related collections. It also includes other filtering and navigation improvements.

For more information, see [View collection relationships](../../clients/manage/collections/view-relationships.md#improvements-in-version-2103).

### Improvements to query preview
<!--8680235-->
You now have more options when using the collection query preview. The following improvements have been made to previewing collection queries:
- Limit the number of rows returned
   - Your limit can be between 1 to 10,000 rows. The default is 5000 rows.
- Omit duplicate rows from the result set
  - If the **Omit duplicate rows** option isn't selected, the original query statement will be executed as is, even if the query contains the word **distinct**.
  - When the **Omit duplicate rows** option is selected, if the query already contains the word **distinct**, then the query runs as it is. When the query doesn't contain the word **distinct**, it's added to the query for the preview (mean override).
- Review statistics for the query preview such as number of rows returned and elapsed time.

For more information, see [How to create collections](../../clients/manage/collections/create-collections.md#bkmk-preview).

### Improvements to collection evaluation view
<!--8787410-->
The following improvements were made to the collection evaluation view:
- The central administration site (CAS) now displays a summary of collection evaluation status for all the primary sites in the hierarchy
- Drill through from collection evaluation status queue to a collection
- Copy text to the clipboard from the collection evaluation page
- Configure the refresh interval for the collection evaluation statistics page

For more information, see [How to view collection evaluation](../../clients/manage/collections/collection-evaluation-view.md).

## Software Center

### Change foreground color for Software Center branding

<!--8655575-->

Software Center already provides various controls for you to customize the branding to support your organization's brand. For some customers, their brand color doesn't work well with the default white font color for a selected item. To better support these customers and improve accessibility, you can now configure a custom color for the foreground font.

For more information, see [About client settings - Software Center](../../clients/deploy/about-client-settings.md#software-center-customization---general).

### Improved user experience and security with Software Center custom tabs

<!--9142301,8655543-->

Since current branch version 1906, you can add up to five custom tabs to Software Center. These custom tabs let you give your users easy access to common web apps and other sites. Previously, to display websites Software Center used the Windows built-in Internet Explorer browser control.

Starting in this release, Software Center can now use the Microsoft Edge WebView2 browser control. The WebView2 browser control provides improved security and user experience. For example, more websites should work with these custom tabs without displaying script errors or security warnings.

For more information, see [About client settings - Software Center](../../clients/deploy/about-client-settings.md#display-custom-tabs-with-microsoft-edge-webview2-runtime).

## Application management

### Disable application deployments

<!--8354812-->

You can now disable application deployments. Other objects already have similar behaviors:

- Software update deployments: Disable the deployment
- Phased deployments: Suspend the phase
- Package: Disable the program
- Task sequence: Disable the task sequence
- Configuration baseline: Disable the baseline

For device-based deployments, when you disable the deployment or object, use the client notification action to **Download Computer Policy**. This action immediately tells the client to update its policy from the site. If the deployment hasn't already started, the client receives the updated policy that the object is now disabled.

For more information, see [Disable and delete application deployments](../../../apps/deploy-use/disable-delete-deployments.md).

## OS deployment

### Windows 10 Servicing dashboard changes
<!--3555940-->
We've simplified the Windows 10 Servicing dashboard to make it more relevant. The new **Quality Update Versions** chart displays the top five revisions of Windows 10 across your devices. The **Latest Feature Update** chart shows the number of devices that installed the latest feature update. The **Windows 10 Usage** chart, showing the distribution of Windows 10 major releases, was renamed to **Feature Update Versions**. Servicing plan and Windows 10 ring information were removed from the dashboard.

For more information, see [Windows 10 servicing dashboard](../../../osd/deploy-use/manage-windows-as-a-service.md#bkmk_2103-dashboard).

### Deploy a feature update with a task sequence

<!--3555906-->

You can now upgrade a client's Windows OS by using a feature update deployed with a task sequence. This integration combines the simplicity of Windows servicing with the flexibility of task sequences. Servicing uses content that you synchronize through the software update point. This process simplifies the need to manually get, import, and maintain the Windows image content used with a standard task sequence to upgrade Windows. The size of the servicing ESD file is generally smaller than the OS upgrade package and WIM image file. You can also use Windows features such as Dynamic Update and Delivery Optimization.

This type of task sequence extends support to Windows 10 on ARM64 devices.

For more information, see the following articles:

- For scenario guidance and planning, see [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).
- For prerequisites, see [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).
- For the new setting on the task sequence step, see [About task sequence steps: Upgrade OS](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

### Task sequence error shows more check readiness details

<!--8888218-->

The task sequence progress can now display more information about readiness checks. If a task sequence fails because the client doesn't meet the requirements configured in the **Check readiness** task sequence step, the user can now see more details about the failed prerequisites.

:::image type="content" source="media/8888218-task-sequence-check-readiness-failure.png" alt-text="Task sequence check readiness failure":::

For more information, see [User experiences for OS deployment](../../../osd/understand/user-experience.md#task-sequence-error).

### Encryption algorithm to capture and restore user state

<!--9171505-->

The task sequence steps to **Capture User State** and **Restore User State** always encrypt the USMT state store. Previously, Configuration Manager configured USMT to use the 3DES algorithm. Starting in this release, both steps now use the highest supported encryption algorithm, **AES 256**.

> [!IMPORTANT]
> If you have any active user state migrations, before you update the Configuration Manager client on those devices, restore the user state. Otherwise, the updated client will fail to restore the user state when it tries to use a different encryption algorithm.

For more information, see [About task sequence steps](../../../osd/understand/task-sequence-steps.md#BKMK_CaptureUserState).

### Improvements to OS deployment

This release includes the following improvements to OS deployment:

- Task sequence conditions now include a **not like** operator. This operator applies to task sequence variable conditions. It's also used in the [Set Dynamic Variable](../../../osd/understand/task-sequence-steps.md#BKMK_SetDynamicVariables) task sequence step.<!--8764365-->

- The [Check Readiness](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) task sequence step now also checks free space on disks without partitions.<!-- 8751864  -->

- The following PowerShell cmdlets now have an **Index** parameter:<!-- 8559060 -->

  - [New-CMOperatingSystemImage](/powershell/module/configurationmanager/new-cmoperatingsystemimage): When you run this cmdlet with the new **Index** parameter, it creates a new single-index image file in the same source folder.
  - [New-CMOperatingSystemInstaller](/powershell/module/configurationmanager/new-cmoperatingsysteminstaller) (alias **New-CMOperatingSystemUpgradePackage**): When you run this cmdlet with the new **Index** parameter, it replaces the original image file in the source folder with a single-index image file.

- The following new cmdlets are available to get the list of existing hardware IDs in the site database:<!-- 8702570 -->

  - **Get-CMDuplicateHardwareIdGuid**
  - **Get-CMDuplicateHardwareIdMacAddress**

  These new cmdlets supplement the existing cmdlets to add and remove duplicate IDs. For more information, see [Version 1910 PowerShell release notes](/powershell/sccm/1910-release-notes#new-cmdlets).

## Protection

### Improvements to BitLocker management

<!--8845996-->

In current branch version 2010, you can manage BitLocker policies and escrow recovery keys over a cloud management gateway (CMG). This support included a couple of limitations.

Starting in this release, BitLocker management policies over a CMG support the following capabilities:

- Recovery keys for removable drives

- TPM password hash, otherwise known as TPM owner authorization

For more information on BitLocker management over CMG, see [Deploy BitLocker management](../../../protect/deploy-use/bitlocker/recovery-service.md).

This release also provides support for the following features:

- Enhanced HTTP<!-- 9503186 -->
- The recovery service on management points that use a database replica.

For more information, see [Plan for BitLocker management](../../../protect/plan-design/bitlocker-management.md).

## Software updates

### Approved scripts for orchestration groups
<!--6991647-->
You can now select from scripts that have already been approved when configuring pre and post-scripts for an [orchestration group](../../../sum/deploy-use/orchestration-groups.md). When in the **Create Orchestration Group Wizard**, you'll see a new page called **Script Picker**. Select your pre and post scripts from your list of scripts that are already approved. You can still add scripts manually on the pre and post-script pages. Additionally, you can also edit scripts that you pre-populated from the **Script Picker**.

For more information, see [Orchestration groups](../../../sum/deploy-use/orchestration-groups.md).

### Change default maximum run time for software updates
<!--7833866-->
Configuration Manager sets the following maximum run time for these categories of software updates:

- **Feature updates for Windows**: 120 minutes
- **Non-feature updates for Windows**: 60 minutes
- **Updates for Microsoft 365 Apps** (Office 365 updates): 60 minutes

All other software updates outside these categories, such as third-party updates, were given a maximum run time of 10 minutes. Starting in Configuration Manager 2103, the default maximum run time for these updates is 60 minutes rather than 10 minutes. The new maximum run time will only apply to new updates that are synchronized from Microsoft Update. It doesn't change the run time on existing updates.

For more information, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime).

### TLS certificate pinning for devices scanning HTTPS-configured WSUS servers
<!--8913032-->
Further increase the security of HTTPS scans against WSUS by enforcing certificate pinning. To fully enable this behavior:
- Ensure your software update points are configured to use TLS/SSL
- Add the certificates for your WSUS servers to the new `WindowsServerUpdateServices` certificate store on your clients
- Verify the **Enforce TLS certificate pinning for Windows Update client for detecting updates** software updates client setting is set to **Yes** (default).

For more information, see [Configure a software update point to use TLS/SSL with a PKI certificate](../../../sum/get-started/software-update-point-ssl.md#bkmk_cert_pinning) and [Client settings for software updates](../../clients/deploy/about-client-settings.md#software-updates).

## Community hub

### Download Power BI report templates from Community hub
<!--5679831-->
Community hub now supports contributing and downloading Power BI report template files. This integration allows administrators to easily share and reuse Power BI reports. Contributing and downloading Power BI report template is also available for current branch versions of Configuration Manager.

For more information, see [Power BI report templates in Community hub](../../servers/manage/powerbi-report-server.md#bkmk_community_hub) and [Using Community hub](../../servers/manage/community-hub.md).

### Download configuration items and configuration baselines from Community hub
<!--7983121-->
You can now download configuration items and configuration baselines from Community hub.

For more information, see [Using Community hub](../../servers/manage/community-hub.md).

### Access the top queries shared in the Community hub from CMPivot
<!--7137169-->

You can now access the top CMPivot queries shared in the Community hub from on-premises CMPivot. By leveraging pre-created CMPivot queries shared by the broader community, CMPivot users gain access to a wider variety of queries. On-premises CMPivot accesses the Community hub and returns a list of the top downloaded CMPivot queries. Users can review the top queries, customize them, and then run on-demand. This improvement gives a wider selection of queries for immediate usage without having to construct them and also allows information sharing on how to build queries for future reference.

For more information, see [Changes to CMPivot in version 2103](../../servers/manage/cmpivot-changes.md#bkmk_2103).

## Configuration Manager console

### Centralized management of console extensions
<!--3555909, 8116426, & 9561090-->

Configuration Manager now supports a new style of console extensions that have the following benefits:

1. Centralized management of console extensions for the site from the console instead of manually placing binaries on individual consoles.
1. A clear separation of console extensions from different extension providers.
1. The ability for admins to have more control over which console extensions are loaded and used in the environment, to keep them more secure.
1. A hierarchy setting that allows for only using the new style of console extension.

The old style of console extensions may start being phased out in favor of the new style, which is more secure and centrally managed.

For more information, see [Console extensions for Configuration Manager](../../servers/manage/admin-console-extensions.md).

### Add a report as a favorite

<!--8034298-->

Configuration Manager ships with several hundred reports by default, and you may have added more to that list. Instead of continually searching for reports you commonly use, you can now make a report a favorite. This action allows you to quickly access it from the new **Favorites** node.

For more information, see [Operations and maintenance for reporting](../../servers/manage/operations-and-maintenance-for-reporting.md#favorites).

### Improvements to the product lifecycle dashboard

<!--8160460-->

This release includes improvements to the product lifecycle dashboard to make it more actionable for you.

- Customize the timeframe on the charts for your preference.
- Search, sort, and filter the data.
- View a list of devices with products that are near or at end of support, and you need to update.

:::image type="content" source="media/8160460-product-lifecycle-timescale.png" alt-text="Product lifecycle dashboard highlighting new timescale control at 33 months":::

For more information, see [product lifecycle dashboard](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).

## Support Center

### Improvements to Support Center

<!--8693068-->

Support Center is now split into the following tools:

- **Support Center Client Data Collector**: Collects data from a device to view in the Support Center Viewer. This separate tool encompasses the existing Support Center action to **Collect selected data**.

- **Support Center Client Tools**: The other Support Center troubleshooting functionality, except for **Collect selected data**.

The following tools are still a part of Support Center:

- **Support Center Viewer**
- **Support Center OneTrace**
- **Support Center Log File Viewer**

For more information, see [Support Center](../../support/support-center.md).

### OneTrace support for jump lists

<!--6991505-->

Support Center OneTrace now supports jump lists for recently opened files. Jump lists let you quickly go to previously opened files, so you can work faster.

There are now three methods to open recent files in OneTrace:

- Windows taskbar jump list
- Windows Start menu recently opened list
- In OneTrace from **File** menu or **Recently opened** tab.

For more information, see [Support Center OneTrace](../../support/support-center-onetrace.md#open-recent-files).

<!-- 
## Content management
 -->

## PowerShell

Starting in version 2103, the ConfigurationManager PowerShell module requires Microsoft .NET version 4.7.2 or later.

### Known issue with updateable PowerShell help

<!-- 8617455 -->

Starting in version 2010, you could use the **Update-Help** cmdlet to download the latest information for the Configuration Manager PowerShell module.

Because of a change in how the updateable content is structured and published with the release of version 2103, don't use **Update-Help** on a version 2010 site. Update the site to version 2103, and then update the local help content.

The cmdlet will successfully download content on a version 2010 console, but **Get-Help** will only return default usage information. Before the release of version 2103, if you used **Update-Help** with a version 2010 site, you can continue to use **Get-Help** now.

For more information, see [PowerShell version 2103 release notes](/powershell/sccm/2103-release-notes#known-issue-with-updateable-powershell-help).

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

The following [features are now deprecated](deprecated/removed-and-deprecated-cmfeatures.md):

- Microsoft Edge legacy [browser profiles](../../../compliance/deploy-use/browser-profiles.md).<!-- 9388900 --> For more information, see [New Microsoft Edge to replace Microsoft Edge Legacy with April’s Windows 10 Update Tuesday release](https://techcommunity.microsoft.com/t5/microsoft-365-blog/new-microsoft-edge-to-replace-microsoft-edge-legacy-with-april-s/ba-p/2114224)

- The following compliance settings for **Company resource access**: <!-- 9315387 -->
  - [Certificate profiles](../../../protect/deploy-use/introduction-to-certificate-profiles.md)
  - [VPN profiles](../../../protect/deploy-use/vpn-profiles.md)
  - [Wi-Fi profiles](../../../protect/deploy-use/create-wifi-profiles.md)
  - [Windows Hello for Business settings](../../../protect/deploy-use/windows-hello-for-business-settings.md)
  - Email profiles

  This deprecation includes the [co-management resource access workload](../../../comanage/workloads.md#resource-access-policies). Use Microsoft Intune to [deploy resource access profiles](../../../../intune/configuration/device-profiles.md).

- Sites that allow HTTP client communication. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

<!--
As first announced in version 1906, version 2103 drops support for the following client OS versions:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise
 -->

## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

- [Remove the central administration site](../../servers/deploy/install/remove-central-administration-site.md) <!-- 3607277 -->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2103 release notes](/powershell/sccm/2103-release-notes).

<!-- For more information on changes to the administration service REST API, see [Administration service release notes](../../../develop/adminservice/release-notes.md). -->

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2103](../../../hotfix/2103/9210721.md).

The following update rollup (10036164) is available in the console starting on June 11, 2021: [Update rollup for Configuration Manager current branch, version 2103](../../../hotfix/2103/10036164.md).

### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [9833643](../../../hotfix/2103/9833643.md) | Console update for Microsoft Endpoint Configuration Manager version 2103 | May 11, 2021 | No |

## Next steps

<!-- At this time, version 2103 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2103.md#early-update-ring). -->

As of April 19, 2021, version 2103 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2103](../../servers/manage/checklist-for-installing-update-2103.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2103.md#post-update-checklist).
