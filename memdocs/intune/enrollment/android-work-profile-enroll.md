---
# required metadata

title: Enroll Android Enterprise work profile devices in Intune
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise work profile devices in Intune.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 5/13/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Set up enrollment of Android Enterprise work profile devices

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune helps you deploy apps and settings to Android Enterprise work profile devices to make sure work and personal information are separate. For specific details about Android Enterprise, see [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

To set up Android Enterprise work profile management, follow these steps:

1. [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md).
2. Specify Android Enterprise work profile enrollment settings. Android Enterprise work profiles are [supported on only certain Android devices](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012%20style=%22target=new_window%22). Any device that supports Android Enterprise work profiles also supports Android device administrator management. Intune lets you specify how devices that support Android Enterprise work profiles should be managed from within [Enrollment Restrictions](enrollment-restrictions-set.md).
    - **Block**:  All Android devices, including devices that support Android Enterprise work profiles, will be enrolled as Android device administrator devices, unless Android device administrator enrollment is also blocked. 
    - **Allow (set by default)**: All devices that support Android Enterprise work profiles are enrolled as Android Enterprise work profile devices. Any Android device that does not support Android Enterprise work profiles is enrolled as an Android device administrator device, unless Android device administrator enrollment is blocked. 
> [!NOTE]
> The default set to **Allow** is true for new tenants as of July 2019. All previous tenants will experience no change to their Enrollment Restrictions, and will see whatever policies they have set in Enrollment Restrictions. For previous tenants that never had Enrollment Restrictions changes, **Block** will still be the default for Android Enterprise work profiles.

3. [Tell your users how to enroll their devices](/intune-user-help/create-a-work-profile-and-enroll-your-device-in-intune-android).  

If you want to enroll devices using Android Enterprise work profiles, but those devices were already enrolled with Android device administrator, those devices must first unenroll and then re-enroll.
> [!NOTE]
> As an administrator, you can accomplish this remotely using the **Retire** function. This function can be found in the actions menu after selecting the device from the **All Devices** blade.

If you're enrolling Android Enterprise work profile devices by using a [Device Enrollment Manager](device-enrollment-manager-enroll.md) account, there is a limit of 10 devices that can be enrolled per account.

For more information, see [Data Intune sends to Google](../intune/protect/data-intune-sends-to-google.md).

## Next steps for Android Enterprise work profiles
- [Deploy Android Enterprise work profile apps](../intune/apps/apps-add-android-for-work.md)
- [Add Android Enterprise work profile configuration policies](../intune/configuration/device-profiles.md)

## See also

[Configuring and troubleshooting Android Enterprise devices in Microsoft Intune](https://support.microsoft.com/help/4476974)
