---
# required metadata

title: Enroll personal devices in Intune with Android Enterprise work profile management 
titleSuffix: Microsoft Intune
description: Learn how to set up Intune for personal devices and bring-your-own-device scenarios using Android Enterprise work profile management. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 2/10/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up enrollment of Android Enterprise personally-owned work profile devices

Enroll personal devices in Microsoft Intune using the *Android Enterprise work profile* management solution for personal-owned devices. During enrollment, a work profile, or partition, is created on the device for work apps and work data. The work profile can be managed by Microsoft Intune policies. Personal apps and data stay separate in another part of the device and remain unaffected by Intune. 

This article describes how to set up device enrollment in Microsoft Intune for work profile management on personal devices. For more information about Android Enterprise work profile features, see [Work profiles](https://support.google.com/work/android/answer/9563584) (opens Android Enterprise Help).  

## Requirements  
* [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md)
* Review [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (opens Google support)  

Any device that supports Android Enterprise personal work profiles also supports the Android device administrator management solution.  

## Set up enrollment  

Complete these steps to set up enrollment and work profile management for personal devices. 

> [!NOTE]
> Device enrollment managers can enroll up to 10 devices per account.     

1. Go to **Devices** > **Android** to set up enrollment restrictions. While configuring [device platform restrictions](create-device-platform-restrictions.md#best-practice---android-platform-restrictions), make sure to allow Android Enterprise work profile management. Your options:    
    - **Block**: Personal devices that enroll will use the Android device administrator management solution, unless device administrator enrollment is also blocked.  
    - **Allow (set by default)**: Personal devices that support the work profile management solution will enroll with a work profile. Android devices that don't support it are enrolled using the Android device administrator solution, unless device administrator enrollment is blocked.  

        > [!NOTE]
        > **Block** is the default setting in policies that you set up prior to July 2019 and never changed.  

2. [Tell your users how to enroll their devices](../user-help/enroll-device-android-work-profile.md). To enroll, users must be using the primary user account on their device. Enrolling with a secondary user account is not supported.  Personal devices previously enrolled with Android device administrator can unenroll, and then re-enroll using the work profile solution.  

> [!TIP]
> You can remotely return a device to a state where it's ready to enroll again by using the **Retire** function in the admin center. To use this remote action, go to **Devices** > **All devices**, and select a device. For more information, see [Retire Android device administrator](../remote-actions/devices-wipe.md#android-device-administrator).    

## Data shared with Google  

For more information, see [Data Intune sends to Google](../protect/data-intune-sends-to-google.md).  

## Next steps
- [Deploy Android Enterprise apps](../apps/apps-add-android-for-work.md)
- [Add Android Enterprise configuration policies](../configuration/device-profiles.md) 
- [Configuring and troubleshooting Android Enterprise devices in Microsoft Intune](https://support.microsoft.com/help/4476974)
