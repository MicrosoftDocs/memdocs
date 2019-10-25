---
title: UUP preview
titleSuffix: Configuration Manager
description: Instructions for preview of UUP integration
ms.date: 10/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
---

# UUP private preview instructions

> [!Note]  
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

## Introduction

The Unified Update Platform (UUP) is the packaging and publishing platform that consumer and enterprise devices use to receive updates from Windows Update for Business. The UUP private preview program is for customers who have agreed to help Microsoft validate the use of UUP updates in Configuration Manager to help solve problems that customers report with servicing Windows today. These updates aren't currently publicly available.

For more information on UUP, see the following Windows blog post: [An update on our Unified Update Platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## Benefits

Windows 10 UUP feature and cumulative updates help solve multiple problems that customers report with servicing Windows today.

### Feature updates

- With a UUP feature update, the Windows update process preserves Features on Demand (FOD) and language packs.

- Update straight to the latest security compliance level. You don't need to install security updates immediately after a feature update. Microsoft publishes a new feature update each month with the latest cumulative security update. You don't need to download or distribute most of the feature update content each month. You only download the security update, which UUP shares with the cumulative update.

### Cumulative updates

- Cumulative updates with UUP include servicing stack updates (SSU) with monthly cumulative security updates. This behavior solves difficulties with orchestrating these two updates. It makes sure that the servicing stack updates are in place to install cumulative updates. You don't need to manage and orchestrate these relationships.

- Cumulative updates with UUP allow for you to distribute FOD and language pack content offline. This behavior enables users to add them on-demand. Users don't need to download from the internet, and you don't need to figure out how to prestage this content.

## Set up

### 1. Send your WSUS ID to Microsoft

To participate in the UUP private preview, share your WSUS ID with your UUP preview contact. Microsoft approves your WSUS environment into the UUP preview program. Without this ID, you're unable to see any UUP updates until the preview is public.

To get your WSUS ID, run the following PowerShell script:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

The **MUUrl** property should be `https://sws.update.microsoft.com`. To change it, see the resolution in the following support article: [WSUS synchronization fails with SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### 2. Update Configuration Manager

Make the following changes to your Configuration Manager site to support this UUP preview:

#### Diagnostics and usage data level

Consider increasing the Configuration Manager diagnostic and data usage level during this preview. The **Full** level helps Microsoft better analyze and troubleshoot issues with this new feature. For more information, see [Levels of diagnostic usage data collection for version 1906](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906).

#### Install the latest update

1. Update the site with one of the following updates:

    - Version 1902 with the [update rollup](https://support.microsoft.com/help/4500571)
    - [Version 1906](/sccm/core/servers/manage/checklist-for-installing-update-1906)

    For more information, see [Install in-console updates](/sccm/core/servers/manage/install-in-console-updates).

2. Update clients.  

    - To simplify this process, consider using automatic client upgrade. For more information, see [Upgrade clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

    - To prevent *unnecessarily downloading around 6 GB* of unused content to the client, update all clients to which you target UUP updates.

### 3. Update Windows clients to a supported version

For UUP updates to install successfully, install both of the following updates:

1. A specific minimum cumulative monthly compliance level.

2. A specific non-cumulative, non-security update from the Microsoft Update Catalog. To import the update into Configuration Manager for deployment, see [Import updates from the Microsoft Update Catalog](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).

#### Supported versions of Windows 10 and required updates

| Windows 10 version | Minimum compliance level | Additional catalog update |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, version 1809** | August 2019, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, version 1803** | April 2019, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, version 1709** | April 2019, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

### 4. Allow clients to download delta content when available

For UUP updates to download correctly, enable the client setting to **Allow clients to download delta content when available**. This setting enables Configuration Manager to let the Windows Update Agent (WUA) determine the necessary content to download to clients. This behavior is instead of the default where the Configuration Manager client downloads all content associated with the UUP update. When you enable this setting, WUA determines the additional content required from each UUP update. For example, only the required FOD and language packs.

When you enable this setting, it doesn't affect server content downloads from the internet. It only applies to client downloads. Before you deploy UUP updates to clients, apply this setting to clients that meet the supported versions for UUP. The prerequisite client updates fix compatibility issues for UUP updates in WSUS and Configuration Manager.

For more information on this client setting, see [About client settings - Software updates](/sccm/core/clients/deploy/about-client-settings#allow-clients-to-download-delta-content-when-available)

### 5. Review your software update infrastructure

Before you synchronize UUP updates, review your automatic deployment rules (ADR) and servicing plans. If you don't want these updates to automatically deploy, revise your ADRs to filter them out. For more information, see [How to find synced UUP updates](#how-to-find-synced-uup-updates). By default, existing servicing plans only deploy non-UUP updates. You can modify the servicing plans to change this behavior.

Review your compliance reports and revise as necessary. For example, if you measure compliance across all products, you'll now see both UUP and non-UUP cumulative updates. Devices will report compliance against both types of updates. Make sure your compliance reports address this change.

## Enable UUP and start testing

### Select products and classifications to sync

Once you're ready to start syncing UUP updates, and Microsoft has approved your WSUS ID, enable the new products:

1. [Synchronize software updates](/sccm/sum/get-started/synchronize-software-updates) to populate the new products.  

2. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

3. Select your top-level site, which is either a central administration site (CAS) or standalone primary site.

4. In the ribbon, select **Configure Site Components**, and choose **Software Update Point**.

5. Switch to the **Products** tab, and select one or more of the following products: 

    - **Windows 10 UUP Preview**
    - **Windows Server UUP Preview**

6. Switch to the **Classifications** tab, and select the following options:  

    - **Security Updates**: To see the UUP cumulative updates  
    - **Upgrades**: To see the UUP feature updates  

7. Synchronize software updates again to see the new UUP updates.

### How to find synced UUP updates

After you have synced UUP updates into your environment, find them in the Configuration Manager console to test. There are two ways to find the preview updates:

- Because these preview updates are in a separate product, use the product to filter to find these updates. Use the servicing plan's product filter to deploy either UUP or non-UUP feature updates.  

- In the **All Software Updates** and **All Windows 10 Updates** nodes of **Software Library**, there's a new optional column **Tag**. This property is also available as a filter in ADRs. For UUP updates, search this field for `UUP`. It's blank for non-UUP updates.  

### Updates available during preview

For more information on all Windows 10 updates released by Microsoft, see [Windows 10 release information](https://docs.microsoft.com/windows/release-information/).

#### Cumulative updates to test

While you might see multiple UUP-tagged updates available, start with the **September 2019** (2019-09) update or a later version. For example:

- 2019-09 Cumulative Update for Windows 10 Version 1809 for x64-based Systems (KB4512578)
- 2019-09 Cumulative Update for Windows 10 Version 1803 for x64-based Systems (KB4516058)
- 2019-09 Cumulative Update for Windows 10 Version 1709 for x64-based Systems (KB4516066)

#### Feature updates to test

While you might see multiple UUP-tagged updates available, start with the **September 2019** (2019-09B) update or a later version. For example:

- Feature update to Windows 10, version 1809 x64 2019-09B
- Feature update to Windows 10, version 1803 x64 2019-09B

## Scenarios to test

### Test feature updates

- Update straight to your chosen security compliance level  

- Install FODs and language packs before the update. Make sure the update preserves these components.  

### Test cumulative updates

During the preview, keep clients compliant using the UUP type update for multiple consecutive updates. This test helps you understand the ongoing behavior.

### Test content

The first update for each major version (1809, 1803, 1709), architecture, and language combination will appear to be large. This size is both in number of files and disk space, compared to what you previously saw with non-UUP updates. This extra content is primarily for all the FOD and language packs for cumulative updates. For feature updates, there's additional large content for that first update.

For future cumulative and feature updates, the amount of new content that the site downloads and distributes is much smaller. UUP intelligently shares all FOD and language pack content between updates. It doesn't need to redownload or redistribute this shared content. During the preview, in Windows 10 versions 1709 and 1803, this monthly download is about the same as the size of the cumulative updates in non-UUP scenarios. In Windows 10 version 1809 and later, the incremental download of the cumulative update is much smaller each month.

When you look at the total content that's downloaded and distributed over a 12-month period for *non-express*, Windows 10 version 1803 without UUP should be about the same as version 1809 with UUP. The total content downloaded and distributed over the entire lifespan of the release is smaller in version 1809 with UUP.

### Supported content channels

For the preview, test your typical real-world scenarios. UUP supports all content channels, including:

- Windows Delivery Optimization (DO)
- Configuration Manager peer cache
- Windows BranchCache
- Use the **No deployment package** option, and clients download straight from Microsoft Update. Use this option with delivery optimization.
- Third-party alternate content providers

For more information, see [Optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).

<!-- TODO: Addlink to WSUS Perf documentation-->
