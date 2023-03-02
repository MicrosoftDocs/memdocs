---
# required metadata

title: Manage Specialty devices with Microsoft Intune
titleSuffix: 
description: This article provides information about specialty devices and how can you manage them with Microsoft Intune
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 03/02/2023
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

Devices management of specialty devices provides a set of device management, configuration, and protection capabilities for purpose-built devices. in

## Specialty devices in Intune  

A device managed by Microsoft Intune is classified as a specialty device if it's included in any of the following categories:

- Large smart screen devices, over 30 inches in size
- AR/VR headsets
- Wearable headsets
- Meeting room devices, a software-based room system that provides an integrated experience for audio conferencing, wireless screen sharing, or video conferencing

The following devices aren't considered specialized devices:

- Laptops and tablet devices
- Foldable messaging devices
- Mobile devices extension such as wearables/watches where the data is managed through mobile apps on iOS and Android mobile phones
- Devices that are included in the plans for frontline workers. See [License Eligibility for Frontline Worker Licenses](https://www.microsoft.com/licensing/terms/en-US/productoffering/Microsoft365/EAEAS)
- IoT devices

## Licensing requirements

Starting March 1, 2023, to use the advanced endpoint management capabilities and remain compliant with the licensing terms of Microsoft agreements you'll need a new license or promotional offer in addition to your plan that includes Microsoft Intune. 

Either a Microsoft Intune Suite, Intune Plan 2, or an alternative Microsoft plan or promotion that covers device licenses is required for users of these devices. The Microsoft Intune Suite and Intune Plan 2 [plans](https://aka.ms/IntuneSuitePricing) are based on a per user per month subscription model and are required to cover all the users of these specialty devices.

- For specialty devices such as headsets and AR/VR devices, you need to purchase either the Microsoft Intune Suite or Intune Plan 2 for the users of these devices. For example, RealWear, HTC, and Meta Qwest 2 devices.  

- For Microsoft devices such as Microsoft Teams Rooms devices, including Microsoft Surface Hub, you must have [Microsoft Teams Room Pro licenses](/microsoftteams/rooms/rooms-licensing) to cover these devices.  

- For [Microsoft HoloLens](windows-holographic-for-business.md), subscribers of Microsoft Intune (Plan1) can access an offer through their Microsoft account teams in the coming months to connect their existing and new devices to Intune Plan 2. In the interim, there's no disruption to your ability to manage and protect HoloLens devices.

- For devices that can run in Microsoft Entra [Azure Active Directory (Azure AD) shared device mode]( /azure/active-directory/develop/msal-shared-devices), you need to have the same volume of Intune Suite or Intune Plan 2 licenses as your core Intune license (Intune Plan 1 for either Microsoft E or F plans) for those users. For example, if 10 frontline workers are sharing one device and they're all covered by Intune Plan 1 licenses, then you would also need to have 10 Intune Plan 2 licenses for these users.

## Next Steps

Learn about enrolling devices into Microsoft Intune here:

- [Enroll devices into Microsoft Intune](../enrollment/device-enrollment.md)