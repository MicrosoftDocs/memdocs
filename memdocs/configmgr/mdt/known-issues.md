---
title: MDT known issues
description: Current limitations with the Microsoft Deployment Toolkit (MDT).
ms.date: 12/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdt
ms.topic: article
ms.assetid: 686f04cd-26f7-4361-a0a3-ddfd8fc4e9a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Microsoft Deployment Toolkit known issues

This article provides details of any current known issues and limitations with the Microsoft Deployment Toolkit (MDT). It assumes familiarity with MDT version concepts, features, and capabilities.

## Windows 10, version 2004

When you use MDT build 8456 with the Windows ADK for Windows 10, version 2004, the BIOS firmware type is incorrectly identified as UEFI. This issue results in failures when refreshing an existing computer with a new version of Windows. To mitigate this issue, install the [MDT hotfix 4564442](https://support.microsoft.com/help/4564442).

## Modern language pack support

Starting with Windows 10 version 1809, language interface packs (LIPs) are delivered as local experience packs (LXPs). LXPs are AppX bundles. When specified in the unattend.xml file, they aren't automatically selected, and the deployment fails. Don't set LXPs as default. Users should select an applied LXP from Windows settings.

## Next steps

[Release notes](release-notes.md)

[Frequently asked questions](faq.md)
