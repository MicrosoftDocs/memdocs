---
# required metadata

title: Manage Intune devices with Android device administrator 
titleSuffix: 
description: Use Android device administrator with Intune to manage devices. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/24/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
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

Android device administrator (sometimes referred to "legacy" Android management and released with Android 2.2) is a way to manage Android devices. However, improved management functionality is available with [Android Enterprise](https://www.android.com/enterprise/management/) in [countries where Android Enterprise is available](https://support.google.com/work/android/answer/6270910). In an effort to move to modern, richer, and more secure device management, Google deprecated Android device administrator management in 2020 and Intune will be ending support for device administrator devices with access to Google Mobile Services in August 2024.

Therefore, we advise against enrolling new devices using the device administrator process described here and we also recommend that you migrate devices off of device administrator management.

For information about using DA when Google Mobile Services are unavailable, see [How to use Intune in environments without Google Mobile Services](../apps/manage-without-gms.md).

[Microsoft Teams certified Android devices](https://learn.microsoft.com/microsoftteams/devices/teams-ip-phones) should no longer be managed with device administrator management and instead should be managed with [AOSP user-associated](android-aosp-corporate-owned-user-associated-enroll.md) management.

If you still decide to have users enroll their Android devices with device administrator management, continue to the next section.

## Set up device administrator enrollment

1. To prepare to manage mobile devices, you must set the mobile device management (MDM) authority to **Microsoft Intune**. See [Set the MDM authority](../fundamentals/mdm-authority-set.md) for instructions. You set this item only once, when you are first setting up Intune for mobile device management.
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose > **Devices** > **Android** > **Android enrollment** > **Personal and corporate-owned devices with device administration privileges** > **Use device administrator to manage devices**.
3. [Tell your users how to enroll their devices](../user-help/enroll-device-android-company-portal.md).  

After a user has enrolled, you can begin managing their devices in Intune, including [assigning compliance policies](../protect/compliance-policy-create-android.md), [managing apps](../apps/app-management.md), and more.

For information about other user tasks, see these articles:
- [Resources about the end-user experience with Microsoft Intune](/mem/intune/fundamentals/intune-planning-guide)
- [Using your Android device with Intune](../user-help/why-enroll-android-device.md)


## Block device administrator enrollment
To block Android device administrator devices, or to block only personally owned Android device administrator devices from enrollment, see [Set device type restrictions](enrollment-restrictions-set.md).


## Next steps
- [Assign compliance policies](../protect/compliance-policy-create-android.md)
- [Managing apps](../apps/app-management.md)
