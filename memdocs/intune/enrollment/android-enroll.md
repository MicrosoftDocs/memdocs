---
# required metadata

title: Enroll Android devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/20/2022
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
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Enroll Android devices  

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

As an Intune administrator, you can enroll Android devices in the following ways:
- Android Enterprise (offering a set of enrollment options that provide users with the most up-to-date and secure features):
    - [**Android Enterprise personally-owned with a work profile**](android-work-profile-enroll.md): For personal devices granted permission to access corporate data. Admins can manage work accounts, apps, and data. Personal data on the device is kept separate from work data and admins don't control personal settings or data. 
    - [**Android Enterprise dedicated**](android-kiosk-enroll.md): For corporate-owned, single use devices, such as digital signage, ticket printing, or inventory management. Admins lock down the usage of a device for a limited set of apps and web links. It also prevents users from adding other apps or taking other actions on the device.
    - [**Android Enterprise fully managed**](android-fully-managed-enroll.md): For corporate-owned, single user devices used exclusively for work and not personal use. Admins can manage the entire device and enforce policy controls unavailable to personally-owned/corporate-owned work profiles.
    - [**Android Enterprise corporate-owned with a work profile**](android-corporate-owned-work-profile-enroll.md): For corporate-owned, single user devices intended for corporate and personal use.
- [**Android device administrator**](android-enroll-device-administrator.md), including Samsung Knox Standard devices and [Zebra devices](../configuration/android-zebra-mx-overview.md). Device administrator should be used in areas where Android Enterprise or Google Mobile Services (GMS) is unavailable.  Google has decreased support for device administrator (DA) management in areas where Android Enterprise is available, and encourages organizations to migrate to Android Enterprise device management. For a list of countries that support Android Enterprise, see [Is Android Enterprise available in my country](https://support.google.com/work/android/answer/6270910)?  
- Android (AOSP) offers a set of enrollment options for devices that aren't integrated with Google Mobile services.  
    - [Corporate-owned, user associated devices](android-aosp-corporate-owned-user-associated-enroll.md): For corporate-owned, single user devices intended exclusively for work and not personal use. Admins can manage the entire device.  
    - [Corporate-owned, userless devices](android-aosp-corporate-owned-userless-enroll.md): For corporate-owned, shared devices. Admins can manage the entire device.  

> [!TIP]
> For guidance on which enrollment method is right for your organization, see [Deployment guide: Enroll Android devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-android.md).

## Prerequisites

To prepare to manage mobile devices, you must set the mobile device management (MDM) authority to **Microsoft Intune**. See [Set the MDM authority](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you’re first setting up Intune for mobile device management.

For Android Enterprise, refer to the following support article from Google to ensure that Android Enterprise is available in your country or region: https://support.google.com/work/android/answer/6270910

For devices manufactured by Zebra Technologies, you may need to grant the Company Portal more permissions depending on the capabilities of the specific device. [Mobility Extensions on Zebra devices](../configuration/android-zebra-mx-overview.md) has more details.

For Samsung Knox Standard devices, there are [more prerequisites](android-samsung-knox-mobile-enroll.md).

## Next steps

- [Set up Android Enterprise personally-owned work profile enrollment](android-work-profile-enroll.md)
- [Set up Android Enterprise dedicated device enrollment](android-kiosk-enroll.md)
- [Set up Android Enterprise fully managed enrollment](android-fully-managed-enroll.md)
- [Set up Android device administrator enrollment](android-enroll-device-administrator.md)
- [Set up Android Enterprise corporate-owned work profile](android-corporate-owned-work-profile-enroll.md)
- [Set up Android (AOSP) corporate-owned user-associated enrollment](android-aosp-corporate-owned-user-associated-enroll.md)
- [Set up Android (AOSP) corporate-owned userless enrollment](android-aosp-corporate-owned-userless-enroll.md)
