---
# required metadata

title: Device restriction settings for Android (AOSP) in Microsoft Intune
description: On Android Open Source Project (AOSP) devices, restrict settings on the device. You can block the camera, block screenshots, disable bluetooth, block USB file transfer, and more in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/25/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

params:
  siblings_only: true
ms.reviewer: priyar, anuragjain
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Android (AOSP) device settings to allow or restrict features using Intune

This article describes the different settings you can control on Android (AOSP) devices. You can use these restrictions to configure password requirements and access to device features.

This feature applies to:

- Android Open Source Project (AOSP) corporate-owned userless devices (shared)  
- Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)  

## Before you begin

- Create an [AOSP device restrictions profile](device-restrictions-configure.md). For the platform, select **Android (AOSP)**.

## Device password  

- **Required password type**: Require users to use a certain type of password. Your options:  

  - **Device default**: To evaluate password compliance, be sure to select a password strength other than **Device default**. If you want to require users to set up a passcode on their devices, configure this setting to a more secure option.  

  - **Numeric** (default): Password must only be numbers, such as `123456789`. Also enter:  

    - **Minimum password length**: Enter the minimum number of digits the password must have, from 4 to 16.  

  - **Numeric complex**: Doesn't permit repeat or consecutive numbers, such as `1111` or `1234`. Also enter:  

    - **Minimum password length**: Enter the minimum number of digits or characters a password must have, from 4 to 16.  

- **Number of sign-in failures before wiping device**: Enter the number of sign-in attempts allowed, from 4 to 11, before the device is wiped. `0` (zero) might disable the device wipe functionality. When the value is blank, Intune doesn't change or update this setting.  

- **Maximum minutes of inactivity until screen locks**: Enter the maximum length of time, from 1 minute to 1 hour, that devices can be idle before the screen is automatically locked. Users must enter their credentials to regain access. For example, enter `5` to lock the device after 5 minutes of inactivity. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.  

> [!NOTE]
>
>- RealWear devices currently only support device default, numeric, and numeric complex password types.  
>- The password type **Password required, no restrictions** appears as an option but doesn't currently work on devices, which is a known issue.

## General

- **Block access to camera**: Prevents access to the camera on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the camera.  

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.  

- **Block screen capture**: Prevents screenshots or screen captures on the device. It also prevents the content from being shown on display devices that don't have a secure video output. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users capture the screen contents as an image.  

- **Disable factory reset**: Prevents users from using the factory reset option in the device's settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow external media on the device.

- **Block mounting of external media**: Prevents users from using or connecting any external media on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to connect external media.  

- **Block USB file transfer**: Prevents users from transferring files over USB. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to transfer files.  

- **Block Wi-Fi setting changes**: Prevents users from creating or changing any Wi-Fi configurations. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the Wi-Fi settings on the device.  

- **Disable Bluetooth**: Disables Bluetooth on the device so that users can't pair with other devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable Bluetooth on the device.

- **Block Bluetooth configuration**: Prevents users from configuring Bluetooth on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to configure Bluetooth.

- **Allow users to turn on debugging features**: Permits users to access the debugging features on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from using the debugging features on the device.

- **Block users from turning on unknown sources**: Prevents users from sideloading apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to sideload apps from unknown sources.

## Related articles

- [Create an Android (AOSP) device compliance policy](../protect/compliance-policy-create-android-aosp.md).
- [Add actions for noncompliant devices](../protect/actions-for-noncompliance.md).  
