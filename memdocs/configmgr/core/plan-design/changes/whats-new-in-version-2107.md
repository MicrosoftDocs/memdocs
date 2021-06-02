---
title: What's new in version 2107
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2107 of Configuration Manager current branch.
ms.date: 07/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby 
---

# What's new in version 2107 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2107 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2002 or later. <!-- baseline only statement: When installing a new site, it will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability.--> This article summarizes the changes and new features in Configuration Manager, version 2107.

> [!NOTE]
> To better align with other releases within Microsoft Endpoint Manager, starting this year the current branch version names will be 2103, 2107, and 2111. They will still release every four months, and release at the same time of the year.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2107](../../servers/manage/checklist-for-installing-update-2107.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2107.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2107+-+Configuration+Manager%22&locale=en-us`


## Staging


## Microsoft Endpoint Manager tenant attach



## Cloud-attached management

### Select VM size for CMG

<!--3555749-->

When you deploy a cloud management gateway (CMG) with a [virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets), you can now choose the virtual machine (VM) size. The following three options are available:

- **Lab**: [B2s](/azure/virtual-machines/sizes-b-series-burstable)
- **Standard**: [A2_v2](/azure/virtual-machines/av2-series). This option continues to be the default setting.
- **Large**: [D2_v3](/azure/virtual-machines/dv3-dsv3-series)

This control gives you greater flexibility with your CMG deployment. You can adjust the size for test labs or if you support large environments. For example, the smaller **Lab** size is ideal for testing with a smaller number of clients at less cost. For production deployments, either use the default **Standard** size or add more capacity with the **Large** size. For more information on how these options differ in cost for your region, see the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/).

<!--
## Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).
 -->

## Site infrastructure


## Real-time management

### Simplified CMPivot permissions requirements
<!--7898885-->
We've simplified the CMPivot permissions requirements. The new permissions are applicable for CMPivot standalone and CMPivot in the on-premises console. The following changes have been made:

- CMPivot no longer requires **SMS Scripts** read permission

  - The [SMS Provider](../hierarchy/plan-for-the-sms-provider.md) still requires this permission if the [administration service](../../../develop/adminservice/overview.md) falls back to it due to a 503 (Service Unavailable) error, as seen in the CMPivot.log.

- The **default scope** permission isn’t required.

### Improvements to CMPivot

<!--9966861-->
We've made the following improvements to CMPivot:

- Added a Key value to the [Registry entity](../../servers/manage/cmpivot-overview.md#bkmk_onprem_only)
- Added a new RegistryKey entity that returns all registry keys matching the given expression
- Added [maxif](/azure/data-explorer/kusto/query/maxif-aggfunction) and [minif](/azure/data-explorer/kusto/query/minif-aggfunction) aggregators that can be used with the [summarize operator](../../servers/manage/cmpivot-overview.md#table-operators)
- Improvements to query autocomplete suggestions in the query editor

## Client management

### Custom properties for devices

<!--8939867-->

Many customers have other data that's external to Configuration Manager but useful for deployment targeting, collection building, and reporting. This data is typically non-technical in nature, not discoverable on the client, and comes from a single external source. For example, a central IT Infrastructure Library (ITIL) system or asset database, which has some of the following device attributes:

- Physical location
- Organizational priority
- Category
- Cost center
- Department

Starting in this release, you can use the [administration service](../../../develop/adminservice/index.yml) to set this data on devices. You can then use the custom properties in Configuration Manager for reporting or to create collections.


### Updated client deployment prerequisite

<!--5170229-->

The Configuration Manager client requires the Microsoft Visual C++ Redistributable component (`vcredist_x*.exe`). When you install the client, it automatically installs this component if it doesn't already exist. Starting in this release, it now uses the Microsoft Visual C++ 2015-2019 Redistributable version 14.28.29914.0. This version improves stability in Configuration Manager client operations.

<!-- For more information, see [Prerequisites for deploying clients to Windows computers](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies). -->

### Hardware inventory for client log settings

<!--5602449-->

You can now inventory client log file settings such as log levels and size. This behavior allows you to track settings that you change by the [Client Diagnostics](../../clients/manage/client-notification.md#client-diagnostics) actions. This new inventory class isn't enabled by default.

<!-- For more information on client log file settings, see [About log files](../../../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions). -->



## Collections


## Software Center

### Software Center notifications display with logo

<!--4993167-->

If you enable Software Center customizations, then notifications on Windows 10 devices display the logo that you configure in client settings. This change helps users to trust these notifications. When you deploy software to a client, the user sees notifications with your logo.


## Application management


## OS deployment

### Support layered keyboard driver during OS deployment

<!--9735002-->

This release adds support for layered keyboard drivers during OS deployment. This driver specifies other types of keyboards that are common with Japanese and Korean languages. For more information, see the [LayeredDriver](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-winpe-layereddriver) setting.

## Protection


## Software updates

### Windows Update native experience for software updates
<!--4316341-->
When installing software updates from Configuration Manager, you can now choose to use the native Windows Update interface and restart experience. The client's Windows Update Settings page will display the updates like they appear when using Windows Update for scanning. Restarts from software updates will also behave as though you're using Windows Update. To use this feature, client devices must be running [Windows Insider build 21277 or later](/windows-insider/active-dev-branch#build-21277).

### Run software updates evaluation from deployment status
<!--9012080 -->

You can now right-click and notify devices to run a software updates evaluation cycle from the [software update deployment status](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUDeployStatus). You can target a single device under the **Asset Details** pane or select a group of devices based on their deployment status.

## Community hub


## Configuration Manager console

### Enhanced code editor
<!--8495588-->
Building on improvements in Configuration Manager 2010 for [syntax highlighting and code folding](../../servers/manage/admin-console-tips.md#bkmk_syntax), you now have the ability to edit scripts in an enhanced editor. The new editor supports syntax highlighting, code folding, word wrap, line numbers, and find and replace. The new editor is available in the console wherever scripts and queries can be viewed or edited.

### Send product feedback from error windows

<!--4262917-->

Previously, if the Configuration Manager console reported an error in a separate window, you had to go back to the main console window to send feedback. In some cases, this action isn't possible with other console windows open.

Starting in this release, error messages include a link to **Report error to Microsoft**. This action opens the standard "send a frown" window to provide feedback. It automatically includes details about the user interface and the error to better help Microsoft engineers diagnose the error. Aside from making it easier to send a frown, it also lets you include the full context of the error message when you share a screenshot.

### Hierarchy approved console extensions don't require signing
<!--9761129-->
Starting in this release, you can choose to allow unsigned [hierarchy approved console extensions](../../servers/manage/admin-console-extensions.md). You may need to allow unsigned console extensions due to an unsigned internally developed extension, or for testing your own custom extension in a lab.

### Configuration Manager console settings aren't saved
<!--5452256-->
When you install the 2107 version of the Configuration Manager console, settings such as column changes, window size, and searches aren't saved. When you first open the upgraded console, it will appear as if it was never previously installed on the device. Any console settings made after installing the 2107 version of the Configuration Manager console will persist when you reopen it.

## Support Center

### Support Center dark and light themes
<!--8218853-->
The [Support Center](../../support/support-center.md) tools now offer dark and light modes. Choose to use the system default color scheme, or override the system default by selecting either the dark or light theme.


### Improvements to Support Center
<!--8272488-->

Starting in this release, the **Content** view in the **Support Center Client Tools** has been renamed to **Deployments**.  From **Deployments**, you can review all of the deployments currently targeted to the device. The new view is grouped by **Category** and **Status**. The view can be sorted and filtered to help you find the deployments you're interested in. Select a deployment in the results pane to display more information in the details pane.

## Tools

### Improvements to CMTrace

<!--9607363-->

This release includes multiple performance improvements to the CMTrace log viewer. Configuration Manager automatically installs this tool in the following locations:

- The site server's tools directory. For example: `cd.latest\SMSSETUP\Tools\CMTrace.exe`
- The Management point's installation directory. For example: `C:\SMS_CCM\CMTrace.exe`
- The client installation directory. For example: `C:\Windows\CCM\CMTrace.exe`
- OS deployment boot images. For example: `X:\sms\bin\x64\CMTrace.exe`

### RBAViewer location change
<!--9579789-->
RBAViewer has moved from `<installdir>\tools\servertools\rbaviewer.exe`. It's now located in the Configuration Manager console directory. After you install the console, RBAViewer.exe will be in the same directory. The default location is `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\rbaviewer.exe`.


<!-- 
## Content management
 -->


## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

As [previously announced](deprecated/removed-and-deprecated-cmfeatures.md), version 2107 drops support for the following features:

- Log Analytics connector for Azure Monitor. This feature was called the _OMS Connector_ in the Azure Services node.


<!--
As first announced in version 1906, version 2107 drops support for the following client OS versions:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise
 -->

## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

- [Remove the central administration site](../../servers/deploy/install/remove-central-administration-site.md) <!-- 3607277 -->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2107 release notes](/powershell/sccm/2107-release-notes).

<!-- For more information on changes to the administration service REST API, see [Administration service release notes](../../../develop/adminservice/release-notes.md). -->

<!-- Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2107](../../../hotfix/2107/9210721.md). -->

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).
-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [9833643](../../../hotfix/2107/9833643.md) | Console update for Microsoft Endpoint Configuration Manager version 2107 | May 11, 2021 | No |
-->

## Next steps

At this time, version 2107 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2107.md#early-update-ring).

<!-- As of April 19, 2021, version 2107 is globally available for all customers to install. -->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2107](../../servers/manage/checklist-for-installing-update-2107.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2107.md#post-update-checklist).
