---
title: Known issues for Windows 365 Enterprise
description: Learn about known issues for Windows 365 Enterprise.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 03/03/2022
audience: Admin
ms.topic: troubleshooting
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection: M365-identity-device-management
---

# Known issues: Windows 365 Enterprise

The following items are known issues for Windows 365 Enterprise.

[!INCLUDE [Missing start menu and taskbar when using iPad and the Remote Desktop app to access a Cloud PC](../includes/known-issues.md)]

## Using resize with restore

A [resize](resize-cloud-pc.md) of a Cloud PC eliminates all existing [restore](restore-overview.md) points for that Cloud PC. New restore points will be captured at the intervals defined in the user setting.

## Restore and automatic rolling credentials

Many devices registered with Active Directory might have a machine account password that is automatically updated. By default, these passwords are updated every 30 days. This automation applies to hybrid joined PCs but not Azure Active Directory Native PCs.

The machine account password is maintained on the Cloud PC. If the Cloud PC is restored to a point that has a previous password stored, the Cloud PC won't be able to sign onto the domain.

For more information, see [Machine Account Password Process](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/machine-account-password-process/ba-p/396026).

## Next steps

[Troubleshoot Windows 365 Enterprise Cloud PC](troubleshooting.md)
