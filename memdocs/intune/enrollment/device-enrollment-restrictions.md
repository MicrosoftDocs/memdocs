---
# required metadata

title: Device enrollment restrictions for the Android Enterprise security configuration framework
titleSuffix: Microsoft Intune
description: Device enrollment restrictions for the Android Enterprise security configuration framework.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
---

# Android Enterprise device enrollment restrictions

Before enrolling devices for the [Android Enterprise security configuration framework](), organizations must configure the appropriate restrictions. These restrictions ensure that users can only enroll
- approved devices.
- a specified number of devices.
- devices with specified platforms.
- devices with specified operating systems.
- devices from specified manufacturers.

For more information on device enrollment restrictions, see [Set enrollment restrictions](enrollment-restrictions-set.md).

## Work profile basic (level 1) security restrictions

For Android Enterprise work profile basic security (Level 1), the following device restrictions must be implemented:

| Type | Platform | Version | Allows personal devices |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade.   Currently, Android recommends Android 8.0 and later for knowledge workers. For more information, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). | Yes |
| Android device administrator| Block | All versions | Yes |

## Work profile high (level 3) security restrictions
For Android Enterprise work profile high security (Level 3), the following device restrictions should be implemented:

| Type | Platform | Version | Allows personal devices |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Android 8.0 and later | Yes |
| Android device administrator| Block | All versions | Yes |

## Fully managed security restrictions
Ensure the organization supports Android Enterprise fully managed device enrollment by reviewing Android Enterprise fully managed enrollment. 

## Next steps

[Work profile security configuration framework settings](android-work-profile-security-settings.md)
[Fully managed security configuration framework settings](android-fully-managed-security-settings.md)