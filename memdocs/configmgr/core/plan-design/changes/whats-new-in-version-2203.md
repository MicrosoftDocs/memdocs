---
title: What's new in version 2203
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2203 of Configuration Manager current branch.
ms.date: 03/01/2203
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
ms.collection: highpri
---

# What's new in version 2203 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2203 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2010 or later. <!-- baseline only statement:--> When installing a new site, it will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability.--> This article summarizes the changes and new features in Configuration Manager, version 2203.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2203](../../servers/manage/checklist-for-installing-update-2203.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2203.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Application management

## Cloud-attached management

## Site infrastructure

## Client management

## Software Center

## Software updates

### Windows Update native experience for software updates
<!--4316341, 10543514-->
When installing software updates from Configuration Manager, you can now choose to use the native Windows Update interface and restart experience. The client's Windows Update Settings page will display the updates like they appear when using Windows Update for scanning. Restarts from software updates will also behave as though you're using Windows Update. When you use the Windows restart experience, you can also brand it for your organization and specify and when forced restarts will occur.

For more information, see [Computer restart client settings](../../clients/deploy/device-restart-notifications.md#bkmk_wu).

## OS deployment

<!--
## Protection
 -->

## Configuration Manager console



## Tools

<!--## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

The following features are deprecated. You can still use them now, but Microsoft plans to end support in the future. -->



## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

<!--
For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2203 release notes](/powershell/sccm/2203-release-notes).

Aside from new features, this release also includes other changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2203](../../../hotfix/2111/11052354.md). -->


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

At this time, version 2203 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2203.md#early-update-ring). 

<!--As of December 15, 2021, version 2111 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2111](../../servers/manage/checklist-for-installing-update-2111.md). --> 

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2111.md#post-update-checklist).
