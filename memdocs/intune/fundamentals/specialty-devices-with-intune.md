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

Specialty device management includes a set of Microsoft Intune management, configuration, and protection capabilities for purpose-built devices such as AR/VR headsets, large smart-screen devices, and select conference room meeting devices. Starting March 1, 2023, to use these advanced endpoint management capabilities and remain compliant with the licensing terms of Microsoft agreements, organizations will need a new license or promotional offer in addition to their plan that includes Microsoft Intune.

Either a Microsoft Intune Suite, Intune Plan 2 or an alternative Microsoft plan or promotion that covers device licenses is required for users of these devices. The new Intune plans are based on a per user per month subscription model and are required to cover all the users of these specialty devices.

For specialty devices such as headsets and AR/VR devices, for example **RealWear** and **HTC** devices, organizations will need to purchase either the Microsoft Intune Suite or Intune Plan 2 for the users of these devices when they are considered generally available.

For **Microsoft Teams Rooms** devices including Microsoft Surface Hub, organizations will need to have sufficient [Microsoft Teams Room Pro licenses]( /microsoftteams/rooms/rooms-licensing), conference area phone [Teams Shared Device license]( /microsoftteams/set-up-common-area-phones) or a Teams license plan that includes Microsoft Intune Plan 1, to cover the users of these devices.  

For **Microsoft HoloLens**, subscribers of Microsoft Intune (Plan 1) will not be required to proactively add the Intune Plan 2 license. Microsoft is exploring ways to use their Microsoft 365 subscription that includes Intune to ensure licensing compliance. In the interim, there will be no disruption to their ability to manage and protect HoloLens devices.

For specialty devices that run in Shared Device Mode (SDM), organizations will need to have the same volume of Intune Suite or Intune Plan 2 licenses as their core Intune license (Intune Plan 1 for either Microsoft E or F plans) for those users. For example, if 10 frontline workers are sharing one device and they are all covered by Intune Plan 1 core licenses, the organization would also need to have 10 Intune Plan 2 licenses.

## Next Steps

Learn about enrolling devices into Microsoft Intune here:

- [Enroll devices into Microsoft Intune](../enrollment/device-enrollment.md)