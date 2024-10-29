---
# required metadata

title: Enroll personal devices in Intune with Android Enterprise work profile management 
titleSuffix: Microsoft Intune
description: Set up Intune for personal devices and bring-your-own-device scenarios using Android Enterprise work profile management. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/28/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
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

# Set up enrollment of Android Enterprise personally owned work profile devices

Set up enrollment for bring-your-own-device (BYOD) and personal device scenarios using the *Android Enterprise personally owned work profile* management solution. During enrollment, a work profile is created on the device to house work apps and work data. You can use Microsoft Intune policies to manage the work profile and its contents. Personal apps and data stay separate in another part of the device and remain unaffected by Intune. 

For more information about Android Enterprise work profile features, see [Work profiles](https://support.google.com/work/android/answer/9563584) (opens Android Enterprise Help).  

## Requirements  
* [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md)
* Review [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (opens Google support)   

## Set up enrollment  

Complete these steps to set up enrollment for Android Enterprise devices in BYOD scenarios. Android Enterprise work profile is allowed by default on personal devices enrolling in Intune. 

> [!NOTE]
> Device enrollment managers can enroll up to 10 devices per account.     

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Go to **Devices** > **Enrollment**.  
3. Select the **Android** tab.  
4. In the **Enrollment options** section, choose **Device platform restriction**.
5. Select the **Android restrictions** tab.  
6. Select **Create restriction**.  
7. On the **Basics** page, enter a name and description for the restriction so that you can distinguish it from other restrictions in the admin center. Device users don't see these details. 
8. Select **Next** to continue to **Platform settings**.  
9. Configure platform settings for **Android Enterprise (work profile)**. Your options:    
    - **Platform**: Select **Allow** to permit enrollment with Android Enterprise work profile. Select **Block** to prevent work profile enrollment. If you block work profile, devices enroll using the Android device administrator management solution, unless device administrator enrollment is also blocked.  
    - **Personally owned**: Select **Allow** to permit personal devices to enroll with a work profile. Personal devices are allowed by default. Select **Block** to prevent personal devices from enrolling with a work profile. Android devices that don't support Android Enterprise enroll using the Android device administrator solution, unless device administrator enrollment is blocked.  

   Any device that supports Android Enterprise personal work profiles also supports the Android device administrator management solution, so if you don't want Android device administrator to be a part of enrollments, make sure to block the platform. For more information, see [device platform restrictions](create-device-platform-restrictions.md#best-practice---android-platform-restrictions).  

     > [!NOTE]
     > Today, Android Enterprise work profile management for personal devices is allowed by default. In policies configured before July 2019 without any changes, the default setting blocks Android Enterprise work profile management.    

     [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]  
     
10. Select **Next** to continue to **Scope tags**.    
11. Optionally, apply one or more scope tags to limit visibility and management of restrictions to certain admin users in Intune. For more information about how to use scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).     
12. Select **Next** to continue to **Assignments**. 
13. Assign the restriction to all users, or select specific groups.  
14. Select **Next** to continue to **Review + create**.  
15. Review your choices, and then select **Create** to finish creating the restriction.  

## Enroll devices  
Communicate enrollment steps to device users. Users typically don't like enrolling themselves, and aren't familiar with the Intune Company Portal app. Be sure to provide guidance, including what information to enter. For some guidance on communicating with your users, see [Planning guide: Step 5 - Create a rollout plan](../fundamentals/intune-planning-guide.md#step-5---create-a-rollout-plan).  

Users must be signed in to the primary user account on their device when enrolling. Enrollment isn't supported on secondary user accounts. Personal devices previously enrolled with Android device administrator can unenroll, and then re-enroll using the work profile solution.  

> [!TIP]
> You can remotely return a device to a state where it's ready to enroll again by using the **Retire** function in the admin center. To use this remote action, go to **Devices** > **All devices**, and select a device. For more information, see [Retire Android device administrator](../remote-actions/devices-wipe.md#android-device-administrator).    

For more information and screenshots of the end user experience, see [Enroll device with Android work profile](../user-help/enroll-device-android-work-profile.md) in the Intune user help docs.    

## Data shared with Google  

Microsoft Intune shares certain user and device information with Google when Android Enterprise device management is enabled. For more information, see [Data Intune sends to Google](../protect/data-intune-sends-to-google.md).  

## Limitations 

The limitations in this section apply to personal devices with a work profile.    

Private space is a feature introduced with Android 15 that lets people create a space on their device for sensitive apps and data they want to keep hidden.   

 * The private space is considered a personal profile. Microsoft Intune doesn't support mobile device management within the private space or provide technical support for devices that attempt to enroll the private space.   

 * If users attempt to enroll the private space after they enroll the device, Intune will initiate the device administrator enrollment process. The second enrollment causes two enrollment records to appear in the Microsoft Intune admin center: one under work profile management and one under device administrator management.  Microsoft Intune doesn't provide support for this scenario.  

## Next steps
- [Deploy Android Enterprise apps](../apps/apps-add-android-for-work.md)
- [Add Android Enterprise configuration policies](../configuration/device-profiles.md) 
- [Configuring and troubleshooting Android Enterprise devices in Microsoft Intune](https://support.microsoft.com/help/4476974)
