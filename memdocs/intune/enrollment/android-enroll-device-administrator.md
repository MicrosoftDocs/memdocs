---
# required metadata

title: Android device administrator enrollment in Microsoft Intune
titleSuffix: 
description: Enroll Android devices into Intune by using device administrator enrollment.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Android device administrator enrollment

Android device administrator (sometimes referred to "legacy" Android management and released with Android 2.2) is a way to manage Android devices. However, improved management functionality is  available with [Android Enterprise](https://www.android.com/enterprise/management/). In an effort to move to modern, richer, and more secure device management, Google is decreasing device administrator support in new Android releases.

Therefore, to avoid such reduced functionality, we advise against enrolling new devices using the device administrator process described below.

For the same reasons, we also recommend that you migrate devices off of device administrator management if the devices are going to update to Android 10. 

> [!IMPORTANT]
> In areas where Android Enterprise is available, Google is encouraging movement off device administrator (DA) management by decreasing its management support in new Android releases. However, where Android Enterprise or Google Mobile Services (GMS) are unavailable, you'll want to use device administrator and familiarize yourself with these changes. For more information, see [Is Android Enterprise available in my country](https://support.google.com/work/android/answer/6270910)?

If you still decide to have users enroll their Android devices with device administrator management, continue to the next section.  

For more information about Google's Android Enterprise features, see these articles:
- [Google's guidance for migration from device administrator to Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google's documentation on the plan to deprecate the device administrator API](https://developers.google.com/android/work/device-admin-deprecation)

## Set up device administrator enrollment

1. To prepare to manage mobile devices, you must set the mobile device management (MDM) authority to **Microsoft Intune**. See [Set the MDM authority](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you are first setting up Intune for mobile device management.
2. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose > **Devices** > **Android** > **Android enrollment** > **Personal and corporate-owned devices with device administration privileges** > **Use device administrator to manage devices**.
3. [Tell your users how to enroll their devices](../user-help/enroll-device-android-company-portal.md).  

After a user has enrolled, you can begin managing their devices in Intune, including [assigning compliance policies](../protect/compliance-policy-create-android.md), [managing apps](../apps/app-management.md), and more.

For information about other user tasks, see these articles:
- [Resources about the end-user experience with Microsoft Intune](../fundamentals/end-user-educate.md)
- [Using your Android device with Intune](../user-help/why-enroll-android-device.md)


## Block device administrator enrollment
To block Android device administrator devices, or to block only personally owned Android device administrator devices from enrollment, see [Set device type restrictions](enrollment-restrictions-set.md).


## Next steps
- [Assign compliance policies](../protect/compliance-policy-create-android.md)
- [Managing apps](../apps/app-management.md)
