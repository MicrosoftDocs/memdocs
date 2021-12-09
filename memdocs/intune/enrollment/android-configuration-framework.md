---
# required metadata

title: Android Enterprise security configuration framework
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings available for Android Enterprise device basic and high security.
keywords:
author: Lenewsad
ms.author: lanewsad
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

# Android Enterprise security configuration framework

The Android Enterprise security configuration framework is a series of recommendations for device compliance and configuration policy settings. These recommendations help you tailor your organization's mobile device security protection to your specific needs.

[!INCLUDE [configuration-framework-1](../includes/configuration-framework-1.md)]

1. [Android Enterprise framework deployment methodology](framework-deployment-methodology.md): A recommended methodology for deploying the security configuration framework.
2. [Android device enrollment restrictions](device-enrollment-restrictions.md): Pre-enrollment device restrictions for Android Enterprise devices.
3. [Set app configuration policies for Android Enterprise devices](android-app-configuration-policies.md): Configure apps on the devices to disallow personal accounts.
4. [Android Enterprise personally-owned/corporate-owned work profile security settings](android-work-profile-security-settings.md): Specific configuration settings for basic and high security on personally-owned/corporate-owned work profile devices.
5. [Android Enterprise fully managed security settings](android-fully-managed-security-settings.md): Specific configuration settings for basic, enhanced, and high security on fully managed devices.

## Android Enterprise enrollment modes

Google Android Enterprise includes two  enrollment modes. The Android Enterprise security configuration framework provides recommendations for both modes.
- [Fully managed devices (device owner)](android-fully-managed-enroll.md): For corporate-owned that are associated with a single user. Such devices are  exclusively for work and not personal use.
- [Personally-owned work profile](android-work-profile-enroll.md) and [Corporate-owned work profile](android-corporate-owned-work-profile-enroll.md) (profile owner): Typically, for personally owned devices where IT wants a clear boundary between work and personal data. Policies controlled by IT make sure that work data can't be transferred into the personal profile.


## Next steps

[Android Enterprise framework deployment methodology](framework-deployment-methodology.md)