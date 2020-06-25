---
# required metadata

title: Android Enterprise security configuration framework
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings suggested for Android Enterprise device basic and high security.
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

# Android Enterprise security configuration framework

Security conscious organizations look at ways to ensure corporate data on mobile devices are protected. One method used to protect that data is through device enrollment. Device enrollment helps organizations deploy:
- compliance policies (like PIN strength, jailbreak/root validation, and so on)
- configuration policies (like WIFI, certificates, VPN).
Device enrollment also enables organizations to manage the app lifecycle.

The number of device compliance and configuration policy settings help you tailor security protection to your specific needs. This flexibility might make it difficult to decide which policy settings are required to implement a complete scenario. To help you set up a complete security scenario, Microsoft has introduced a new taxonomy for [security configurations in Windows 10](https://aka.ms/secconframework). Intune is using a similar taxonomy for its Android Enterprise security configuration framework. This taxonomy is explained below and in the following articles:

1. [Android Enterprise framework deployment methodology](framework-deployment-methodology.md): An explanation of a recommended configuration deployment methodology.
2. [Android device enrollment restrictions](device-enrollment-restrictions.md): Pre-enrollment device restrictions for Android Enterprise devices.
3. [Set app configuration policies for Android Enterprise devices](android-app-configuration-policies.md): Configure apps on the devices to disallow personal accounts.
4. [Android Enterprise work profile security settings](android-work-profile-security-settings.md): Specific configuration settings for basic and high security on work profile devices.
5. [Android Enterprise fully managed security settings](android-fully-managed-security-settings.md): Specific configuration settings for basic, enhanced, and high security on fully managed devices.



## Android Enterprise enrollment modes

With Android 5.0, Google introduced Android Enterprise which includes two  enrollment modes:
- [Fully managed devices (device owner)](android-fully-managed-enroll.md): For corporate-owned that are associated with a single user. Such devices are  exclusively for work and not personal use.
- [Work profile (profile owner)](android-work-profile-enroll.md): Typically, for personally-owned devices where IT wants a clear boundary between work and personal data. Policies controlled by IT make sure that work data cannot be transferred into the personal profile.


## Next steps

[Android Enterprise framework deployment methodology](framework-deployment-methodology.md)