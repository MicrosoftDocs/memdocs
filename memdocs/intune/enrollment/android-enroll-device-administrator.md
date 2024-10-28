---
# required metadata

title: Manage Intune devices with Android device administrator 
titleSuffix: 
description: Use Android device administrator with Intune to manage devices. 
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

ms.reviewer: esalter
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Android device administrator enrollment  

 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]  

Android device administrator (sometimes referred to *legacy* Android management and released with Android 2.2) is a way to manage Android devices. However, improved management functionality is available with [Android Enterprise](https://www.android.com/enterprise/management/) in [countries/regions where Android Enterprise is available](https://support.google.com/work/android/answer/6270910). Google deprecated Android device administrator management in 2020. Intune is ending support for device administrator devices with access to Google Mobile Services at the end of 2024.  

Therefore, we advise against enrolling new devices using the device administrator process described here and we also recommend that you migrate devices off of device administrator management.

For information about using device administrator when Google Mobile Services is unavailable, see [How to use Intune in environments without Google Mobile Services](../apps/manage-without-gms.md). 

If you still decide to have users enroll their Android devices with device administrator management, continue to the next section.

## Set up device administrator enrollment

1. To prepare to manage mobile devices, you must set the mobile device management (MDM) authority to **Microsoft Intune**. See [Set the MDM authority](../fundamentals/mdm-authority-set.md) for instructions. You only need to configure this setting in your tenant once.  
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Go to **Devices** > **Enrollment.
4. Select the **Android** tab.
5. Under **Android device administrator**, choose **Personal and corporate-owned devices with device administration privileges**.
6. Select the checkmark next to **Use device administrator to manage devices**.  
7. [Tell your users how to enroll their devices](../user-help/enroll-device-android-company-portal.md).  

After a user enrolls, you can begin managing their devices in Intune, including [assigning compliance policies](../protect/compliance-policy-create-android.md), [managing apps](../apps/app-management.md), and more.

For information about other user tasks, see these articles:  

- [Microsoft Intune planning guide](../fundamentals/intune-planning-guide.md)  

- [Android device enrollment overview ](../user-help/why-enroll-android-device.md)  

## Block device administrator enrollment
To block Android device administrator devices, or to block only personally owned Android device administrator devices from enrollment, see [Set device type restrictions](enrollment-restrictions-set.md).

## Microsoft Teams certified Android devices

[Microsoft Teams certified Android devices](/microsoftteams/devices/teams-ip-phones) should continue being managed with device administrator management until [AOSP user-associated](android-aosp-corporate-owned-user-associated-enroll.md) management becomes available for these devices.  

To unenroll a Microsoft Teams-certified Android device you manage with Android device administrator, you must:  

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/).
1. Deselect the Intune license from the Teams account for the Android device. 

After you remove an Intune license, there's a 30 day grace period, during which the device still functions. The device must sign in again after this step to avoid enrolling in Intune under device administrator management again. 

## Limitations 

The limitations in this section apply to devices managed with device administrator.    

Private space is a feature introduced with Android 15 that lets people create a space on their device for sensitive apps and data they want to keep hidden. 

 * The private space is considered a personal profile. Microsoft Intune doesn't support mobile device management within the private space or provide technical support for devices that attempt to enroll the private space.   

 * Users might try to create a work profile-like experience on their devices by enrolling only the private space, leading to partial device management. Microsoft Intune doesn't provide support for this scenario. 

 * After a user enrolls their personal device, if they attempt to enroll the private space, Intune will initiate the personal work profile enrollment flow. However, in this scenario the enrollment process will fail without any notification.    

## Next steps
- [Assign compliance policies](../protect/compliance-policy-create-android.md)
- [Managing apps](../apps/app-management.md)
