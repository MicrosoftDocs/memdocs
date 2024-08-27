---
# required metadata
title: Remotely manage Windows 365 devices
titleSuffix:
description: Learn how to remotely manage Windows 365 devices.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/27/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Remotely manage Windows 365 devices

You can remotely manage Cloud PCs in Intune just like any other managed device. For more information, see [Remotely run device actions with Intune](/mem/intune/remote-actions/).

Cloud PCs support the following remote management actions:

| Remote action | Bulk action support? |
| --- | :---: |
| [Collect diagnostics](/mem/intune/remote-actions/collect-diagnostics) | Yes |
| Create Cloud PC manual restore point | Yes |
| Full Scan | No |
| [Place Cloud PC Under Review](place-cloud-pc-under-review.md) | Yes |
| Power Off (Windows 365 Frontline) (preview) | Yes |
| Power On (Windows 365 Frontline) (preview) | Yes |
| Quick Scan | No |
| [Remove Cloud PCs from review](place-cloud-pc-under-review.md) | Yes |
| Rename | No |
| [Reprovisioning](provisioning.md#reprovisioning) | Yes |
| [Resize](resize-cloud-pc.md) | Yes |
| Restart | Yes |
| [Restore](restore-overview.md) | Yes|
| Share Cloud PC restore point to storage | Yes |
| Sync | Yes |
| [Troubleshoot](health-checks-connectivity.md) | Yes |
| Update Windows Defender | No |

You can run remote actions for up to 5,000 Cloud PCs at a time. For more information about bulk actions, see [Use bulk device actions](/mem/intune/remote-actions/bulk-device-actions).

## Windows 365 Frontline Cloud PCs

Frontline Cloud PCs support remote actions like Enterprise Cloud PCs. One difference is that a Frontline Cloud PC power state is determined by the end user. When a Frontline Cloud PC is on, remote actions are started immediately. If a Frontline Cloud PC is powered off, remote actions start as soon as the Cloud PC is powered on. When a Cloud PC is powered on, it uses a license that others can't use. When the Cloud PC is powered off, the license is freed up so others can use it.

You can view the power state for Frontline Cloud PCs in the Intune portal on the devices **Properties** page.

You can remotely power on and off a Frontline Cloud PC. When you power on a Frontline Cloud PC, a license is automatically consumed. When you power off a Frontline Cloud PC:

- Any user currently signed in is signed off.
- Unsaved data on the Cloud PC is lost.

You can also power on and power off Frontline Cloud PCs in bulk to help with:

- Run an update.
- Apply an application across all Cloud PCs.
- Make sure Cloud PCs are on for an incoming shift.
- Manage concurrency limits.

Within the Intune portal, you can get to the bulk actions tab by going to **Devices**> **All devices** > **Bulk device actions**.  

<!-- ########################## -->
## Next steps

[Reprovision a Cloud PC](reprovision-cloud-pc.md).
