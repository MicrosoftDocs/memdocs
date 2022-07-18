---
# required metadata

title: Device enrollment restrictions for the Android Enterprise security configuration framework
titleSuffix: Microsoft Intune
description: Device enrollment restrictions for the Android Enterprise security configuration framework.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/03/2021
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

# Android Enterprise device enrollment restrictions for personally owned work profile devices

Before enrolling Android Enterprise personally owned work profile devices for the [Android Enterprise security configuration framework](android-configuration-framework.md), organizations must configure the appropriate restrictions. These restrictions ensure that users can only enroll

- approved devices.
- a specified number of devices.
- devices with specified platforms.
- devices with specified operating systems.
- devices from specified manufacturers.

For more information on device enrollment restrictions, see [Set enrollment restrictions](enrollment-restrictions-set.md).

## Personally owned work profile basic (level 1) security restrictions

For Android Enterprise personally owned work profile basic security (Level 1), the following device restrictions must be implemented:

| Type | Platform | Version | Allows personal devices |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Android 8.0 and later.<p>Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade.   Currently, Android recommends Android 9.0 and later for knowledge workers. For more information, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). | Yes |
| Android device administrator| Block | All versions | Yes |

## Personally owned work profile high (level 3) security restrictions
For Android Enterprise personally owned work profile high security (Level 3), the following device restrictions should be implemented:

| Type | Platform | Version | Allows personal devices |
|--------|--------|--------|--------|
| Android Enterprise | Allow | Android 9.0 and later | Yes |
| Android device administrator| Block | All versions | Yes |

## Fully managed security restrictions
Ensure the organization supports Android Enterprise fully managed device enrollment by reviewing [Enroll the fully managed devices](android-fully-managed-enroll.md#enroll-the-fully-managed-devices). 

## Conditional access policies
Organizations can use Azure AD Conditional Access policies to ensure that users can only access work or school content on enrolled Android devices. To do this, you will need a conditional access policy that targets all potential users. Details on creating this policy can be found in [Require managed devices for cloud app access with Conditional Access](/azure/active-directory/conditional-access/require-managed-devices).

Follow the steps in [Scenario: Require device enrollment for iOS and Android devices](/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices), which ensures that only enrolled mobile devices that are compliant can connect to  Microsoft 365 endpoints.

## Next steps

[Set app configuration policies](android-app-configuration-policies.md)
