---
# required metadata

title: Enroll Android devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android devices in Intune.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 11/9/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: f276d98c-b077-452a-8835-41919d674db5

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18 
ms.collection: M365-identity-device-management
---

# Enroll Android devices

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

As an Intune administrator, you can enroll Android devices in the following ways:
- Android Enterprise (offering a set of enrollment options that provide users with the most up-to-date and secure features):
    - [**Android Enterprise personally-owned with a work profile**](android-work-profile-enroll.md): For personal devices granted permission to access corporate data. Admins can manage work accounts, apps, and data. Personal data on the device is kept separate from work data and admins don't control personal settings or data. 
    - [**Android Enterprise dedicated**](android-kiosk-enroll.md): For corporate-owned, single use devices, such as digital signage, ticket printing, or inventory management. Admins lock down the usage of a device for a limited set of apps and web links. It also prevents users from adding other apps or taking other actions on the device.
    - [**Android Enterprise fully managed**](android-fully-managed-enroll.md): For corporate-owned, single user devices used exclusively for work and not personal use. Admins can manage the entire device and enforce policy controls unavailable to personally-owned/corporate-owned work profiles.
    - [**Android Enterprise corporate-owned with a work profile**](android-corporate-owned-work-profile-enroll.md): For corporate-owned, single user devices intended for corporate and personal use.
- [**Android device administrator**](android-enroll-device-administrator.md), including Samsung Knox Standard devices and [Zebra devices](../configuration/android-zebra-mx-overview.md). In areas where Android Enterprise is available, Google is encouraging movement off device administrator (DA) management by decreasing its management support in new Android releases. However, where Android Enterprise or Google Mobile Services (GMS) are unavailable, you'll want to use device administrator and familiarize yourself with these changes. For more information, see [Is Android Enterprise available in my country](https://support.google.com/work/android/answer/6270910)?

## Prerequisites

To prepare to manage mobile devices, you must set the mobile device management (MDM) authority to **Microsoft Intune**. See [Set the MDM authority](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you are first setting up Intune for mobile device management.

For Android Enterprise, refer to the following support article from Google to ensure that Android Enterprise is available in your country or region: https://support.google.com/work/android/answer/6270910

For devices manufactured by Zebra Technologies, you may need to grant the Company Portal additional permissions depending on the capabilities of the specific device. [Mobility Extensions on Zebra devices](../configuration/android-zebra-mx-overview.md) has more details.

For Samsung Knox Standard devices, there are [more prerequisites](android-samsung-knox-mobile-enroll.md).

## Next steps

- [Set up Android Enterprise personally-owned work profile enrollments](android-work-profile-enroll.md)
- [Set up Android Enterprise dedicated device enrollments](android-kiosk-enroll.md)
- [Set up Android Enterprise fully managed enrollments](android-fully-managed-enroll.md)
- [Set up Android device administrator enrollment](android-enroll-device-administrator.md)
- [Set up Android Enterprise corporate-owned work profile**](android-corporate-owned-work-profile-enroll.md)
