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

## Microsoft Endpoint Manager tenant attach


<!-- 
## Cloud-attached management

## Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).
 -->

## Site infrastructure


<!-- 
## Client management
 -->


## Collections


## Software Center


## Application management


## OS deployment


## Protection


## Software updates


## Community hub


## Configuration Manager console


## Support Center


<!-- 
## Content management
 -->


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
