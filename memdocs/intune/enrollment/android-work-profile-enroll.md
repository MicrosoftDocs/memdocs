---
# required metadata

title: Enroll personal devices in Intune with Android Enterprise work profile management 
titleSuffix: Microsoft Intune
description: Learn how to set up Intune for personal devices and bring-your-own-device scenarios using Android Enterprise work profile management. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 3/24/2023
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

Set up enrollment for bring-your-own-device (BYOD) and personal device scenarios using the *Android Enterprise personally-owned work profile* management solution. During enrollment, a work profile is created on the device to house work apps and work data. The work profile can be managed by Microsoft Intune policies. Personal apps and data stay separate in another part of the device and remain unaffected by Intune. 

For more information about Android Enterprise work profile features, see [Work profiles](https://support.google.com/work/android/answer/9563584) (opens Android Enterprise Help).  

## Requirements  
* [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md)
* Review [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (opens Google support)   

## Set up enrollment  

Complete these steps to set up enrollment for Android Enterprise devices in BYOD scenarios.  

> [!NOTE]
> Device enrollment managers can enroll up to 10 devices per account.     

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **Enrollment device platform restrictions** to set up enrollment restrictions. By default, Android Enterprise work profile is marked as allowed for personal devices enrolling in Intune. You can allow or block enrollment in device platform restrictions.  Your options:    
    - **Block**: Personal devices that enroll will use the Android device administrator management solution, unless device administrator enrollment is also blocked.  
    - **Allow (set by default)**: Personal devices that support the work profile management solution will enroll with a work profile. Android devices that don't support Android Enterprise are enrolled using the Android device administrator solution, unless device administrator enrollment is blocked.  

   Any device that supports Android Enterprise personal work profiles also supports the Android device administrator management solution, so if you don't want Android device administrator to be a part of enrollments, make sure to block the platform. For more information, see [device platform restrictions](create-device-platform-restrictions.md#best-practice---android-platform-restrictions).  

     > [!NOTE]
     > Today, Android Enterprise work profile management for personal devices is allowed by default. In policies configured before July 2019 without any changes, the default setting blocks Android Enterprise work profile management.    

3. Communicate enrollment steps to device users. Users typically don't like enrolling themselves, and may not be familiar with the Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Step 5 - Create a rollout plan](../fundamentals/intune-planning-guide.md#step-5---create-a-rollout-plan).  

     Users must be signed in to the primary user account on their device when enrolling. Enrollment is not supported on secondary user accounts. Personal devices previously enrolled with Android device administrator can unenroll, and then re-enroll using the work profile solution.  

     > [!TIP]
     > You can remotely return a device to a state where it's ready to enroll again by using the **Retire** function in the admin center. To use this remote action, go to **Devices** > **All devices**, and select a device. For more information, see [Retire Android device administrator](../remote-actions/devices-wipe.md#android-device-administrator).    

     For more information and screenshots of the end user experience, see [Enroll device with Android work profile](../user-help/enroll-device-android-work-profile.md) in the Intune user help docs.    

## Data shared with Google  

Microsoft Intune shares certain user and device information with Google when Android Enterprise device management is enabled.  For more information, see [Data Intune sends to Google](../protect/data-intune-sends-to-google.md).  

## Next steps
- [Deploy Android Enterprise apps](../apps/apps-add-android-for-work.md)
- [Add Android Enterprise configuration policies](../configuration/device-profiles.md) 
- [Configuring and troubleshooting Android Enterprise devices in Microsoft Intune](https://support.microsoft.com/help/4476974)
