---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-device-group.md
pre-provisioning/hybrid-azure-ad-join-device-group.md
self-deploying/self-deploying-device-group.md
user-driven/azure-ad-join-device-group.md
user-driven/hybrid-azure-ad-join-device-group.md

Headings are driven by article context. -->

Device groups are a collection of devices organized into a Microsoft Entra group. Device groups are used in Autopilot to target devices for specific configurations such as what policies to apply to a device and what applications to install on the device. They're also used by Autopilot to target Enrollment Status Page (ESP) configurations, Autopilot profile configurations, and domain join profiles to devices.

Device groups can be either dynamic or assigned:

- **Dynamic groups** - Devices are automatically added to the group based on rules
- **Assigned groups** - Devices are manually added to the group and are static

When an admin configures Autopilot in an enterprise environment, dynamic groups are primarily used since a large number of devices are normally involved. Adding the devices in automatically using rules makes management of the group a lot easier. Adding a large amount of device in manually via an assigned group would be impractical. However, if there's only a few devices, for example for testing purposes, an assigned group can be used instead.

To create a dynamic device group for use with Autopilot, follow these steps:
