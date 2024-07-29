---
# required metadata

title: Manage Intune devices with Android device administrator 
titleSuffix: 
description: Use Android device administrator with Intune to manage devices. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/05/2024
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

Android device administrator (sometimes referred to *legacy* Android management and released with Android 2.2) is a way to manage Android devices. However, improved management functionality is available with [Android Enterprise](https://www.android.com/enterprise/management/) in [countries where Android Enterprise is available](https://support.google.com/work/android/answer/6270910). In an effort to move to modern, richer, and more secure device management, Google deprecated Android device administrator management in 2020 and Intune will be ending support for device administrator devices with access to Google Mobile Services at the end of 2024.

Therefore, we advise against enrolling new devices using the device administrator process described here and we also recommend that you migrate devices off of device administrator management.

For information about using device administrator when Google Mobile Services is unavailable, see [How to use Intune in environments without Google Mobile Services](../apps/manage-without-gms.md). 

If you still decide to have users enroll their Android devices with device administrator management, continue to the next section.

## Set up device administrator enrollment

1. To prepare to manage mobile devices, you must set the mobile device management (MDM) authority to **Microsoft Intune**. See [Set the MDM authority](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you are first setting up Intune for mobile device management.
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Go to **Devices** > **Enrollment.
4. Select the **Android** tab.
5. Under **Android device administrator**, choose **Personal and corporate-owned devices with device administration privileges**.
6. Select the checkmark next to **Use device administrator to manage devices**.  
7. [Tell your users how to enroll their devices](../user-help/enroll-device-android-company-portal.md).  

After a user has enrolled, you can begin managing their devices in Intune, including [assigning compliance policies](../protect/compliance-policy-create-android.md), [managing apps](../apps/app-management.md), and more.

For information about other user tasks, see these articles:
- [Resources about the end-user experience with Microsoft Intune](../fundamentals/intune-planning-guide.md)
- [Using your Android device with Intune](../user-help/why-enroll-android-device.md)  

## Block device administrator enrollment
To block Android device administrator devices, or to block only personally owned Android device administrator devices from enrollment, see [Set device type restrictions](enrollment-restrictions-set.md).

## Microsoft Teams certified Android devices

[Microsoft Teams certified Android devices](/microsoftteams/devices/teams-ip-phones) should continue being managed with device administrator management until [AOSP user-associated](android-aosp-corporate-owned-user-associated-enroll.md) management becomes available for these devices.  

To unenroll a Microsoft Teams certified Android device that's enrolled in Android device administrator, sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/) and deselect the Intune license from the Teams account for the Android device. After you remove an Intune license, there is a 30 day grace period in which the device still functions. The device will have to sign in again after this step to avoid enrolling in Intune under device administrator management again. 

## Next steps
- [Assign compliance policies](../protect/compliance-policy-create-android.md)
- [Managing apps](../apps/app-management.md)
