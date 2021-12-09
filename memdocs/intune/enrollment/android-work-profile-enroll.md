---
# required metadata

title: Enroll Android Enterprise personally-owned work profile devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise personally-owned work profile devices in Intune.
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

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Set up enrollment of Android Enterprise personally-owned work profile devices

Intune helps you deploy apps and settings to Android Enterprise personally-owned work profile devices to make sure work and personal information are separate. For specific details about Android Enterprise, see [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

To set up [Android Enterprise personally-owned work profile](../apps/android-deployment-scenarios-app-protection-work-profiles.md#android-enterprise-personally-owned-work-profiles) management, follow these steps:

1. [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md).
2. Specify Android Enterprise work profile enrollment settings. Android Enterprise personally-owned work profiles are [supported on only certain Android devices](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012%20style=%22target=new_window%22). Any device that supports Android Enterprise personally-owned work profiles also supports Android device administrator management. Intune lets you specify how devices that support work profiles should be managed from within [Enrollment Restrictions](enrollment-restrictions-set.md).
    - **Block**:  All Android devices will be enrolled as Android device administrator devices, unless device administrator enrollment is also blocked. This behavior includes devices that support Android Enterprise personally-owned work profiles.
    - **Allow (set by default)**: All devices that support Android Enterprise personally-owned work profiles are enrolled as personally-owned work profile devices. Any Android device that doesn't support personally-owned work profiles is enrolled as an Android device administrator device, unless device administrator enrollment is blocked. 
> [!NOTE]
> The default set to **Allow** is true for new tenants as of July 2019. All previous tenants will experience no change to their Enrollment Restrictions, and will see whatever policies they have set in Enrollment Restrictions. For previous tenants that never had Enrollment Restrictions changes, **Block** will still be the default for personally-owned work profiles.

3. [Tell your users how to enroll their devices](../user-help/enroll-device-android-work-profile.md). To enroll, users must be using the primary user account on their device. Enrolling with a secondary user account is not supported.     

Devices previously enrolled with Android device administrator can be re-enrolled using personally-owned work profiles. You'll first need to unenroll the device administrator devices. Then you can re-enroll them with personally-owned work profiles.

> [!NOTE]
> As an administrator, you can accomplish this remotely using the **Retire** function. This function can be found in the actions menu after selecting the device from the **All Devices** blade.

If you're enrolling personally-owned work profile devices by using a [Device Enrollment Manager](device-enrollment-manager-enroll.md) account, there's a limit of 10 devices that can be enrolled per account.

For more information, see [Data Intune sends to Google](../protect/data-intune-sends-to-google.md).

## Next steps
- [Deploy Android Enterprise apps](../apps/apps-add-android-for-work.md)
- [Add Android Enterprise configuration policies](../configuration/device-profiles.md)

## See also

[Configuring and troubleshooting Android Enterprise devices in Microsoft Intune](https://support.microsoft.com/help/4476974)
