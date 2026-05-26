---
title: Manage Specialty devices with Microsoft Intune
description: This article provides information about specialty devices and how can you manage them with Microsoft Intune
author: lenewsad
ms.author: lanewsad
ms.date: 05/12/2026
ms.topic: article
ms.reviewer: priyar
ms.subservice: suite
ms.collection:
- M365-identity-device-management
---

# Specialty device management

Specialty device management provides a range of management, configuration, and protection capabilities for specialized devices, such as AR/VR headsets, large smart-screen devices, and select conference room meeting devices.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

>[!INCLUDE [additional-licensing-plan2](../includes/licensing/additional-licensing-plan2.md)]
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::
> Specialty device management is supported in the following cloud environments:
> - Public cloud
> - Sovereign cloud environments:
>   - U.S. Government Community Cloud (GCC) High
>   - U.S. Department of Defense (DoD)
:::column-end:::
:::row-end:::

### Licensing considerations

For specialty devices such as headsets and AR/VR devices, for example **Apple Vision Pro**, **RealWear**, and **HTC** devices, organizations must assign a required license to the users of these devices. 

For **Microsoft Teams Rooms** devices including Microsoft Surface Hub, organizations need to have sufficient [Microsoft Teams Rooms Pro licenses](/microsoftteams/rooms/rooms-licensing), conference area phone [Teams Shared Device license](/microsoftteams/set-up-common-area-phones) or a Teams license plan that includes Microsoft Intune Plan 1, to cover the users of these devices.

For **Microsoft HoloLens**, subscribers of Microsoft Intune (Plan 1) aren't required to add more licenses to manage HoloLens devices.

For specialty devices that run in Microsoft Entra shared device Mode (SDM), organizations need to have the same volume of required licenses as their core Intune license (Intune Plan 1 for either Microsoft E or F plans) for those users. For example, if 10 frontline workers are sharing one device and they're all covered by Intune Plan 1 core licenses, the organization should also have 10 of the required specialty device licenses to cover those users.

## Next Steps

Learn about enrolling devices into Microsoft Intune here:

- [Enroll devices into Microsoft Intune](../device-enrollment/guide.md)
