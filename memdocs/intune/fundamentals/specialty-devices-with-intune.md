---
# required metadata

title: Manage Specialty devices with Microsoft Intune
titleSuffix: 
description: This article provides information about specialty devices and how can you manage them with Microsoft Intune
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/07/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started; seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Managing specialty devices with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Specialty device management with Microsoft Intune provides a range of management, configuration, and protection capabilities for specialized devices, such as AR/VR headsets, large smart-screen devices, and select conference room meeting devices. To use these advanced endpoint management capabilities and remain compliant with the licensing terms of Microsoft agreements, organizations will need a new license or promotional offer in addition to their plan that includes Microsoft Intune, starting from March 1, 2023.

Either a Microsoft Intune Suite, Intune Plan 2 or an alternative Microsoft plan or promotion that covers device licenses is required for users of these devices. The new Intune plans are based on a per user per month subscription model and are required to cover all the users of these specialty devices.

For specialty devices such as headsets and AR/VR devices, for example **RealWear** and **HTC** devices, organizations need to purchase either the Microsoft Intune Suite or Intune Plan 2 for the users of these devices when they're considered generally available.

For **Microsoft Teams Rooms** devices including Microsoft Surface Hub, organizations need to have sufficient [Microsoft Teams Room Pro licenses](https://learn.microsoft.com/microsoftteams/rooms/rooms-licensing), conference area phone [Teams Shared Device license](https://learn.microsoft.com/microsoftteams/set-up-common-area-phones) or a Teams license plan that includes Microsoft Intune Plan 1, to cover the users of these devices.  
[text here](mi)
For **Microsoft HoloLens**, subscribers of Microsoft Intune (Plan 1) aren't required to proactively add the Intune Plan 2 license. Microsoft is exploring ways to use their Microsoft 365 subscription that includes Intune to ensure licensing compliance. In the interim, there won't be any disruption to their ability to manage and protect HoloLens devices.

For specialty devices that run in Shared Device Mode (SDM), organizations need to have the same volume of Intune Suite or Intune Plan 2 licenses as their core Intune license (Intune Plan 1 for either Microsoft E or F plans) for those users. For example, if 10 frontline workers are sharing one device and they're all covered by Intune Plan 1 core licenses, the organization should also  have 10 Intune Plan 2 licenses.

## Next Steps

Learn about enrolling devices into Microsoft Intune here:

- [Enroll devices into Microsoft Intune](../enrollment/device-enrollment.md)