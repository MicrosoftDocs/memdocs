---
# required metadata

title: Android configuration list for Intune settings catalog
description: Use the Microsoft Intune settings catalog to add, configure, or restrict features on Android devices. This article lists and describes the settings you can configure.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: laurawi
ms.date: 06/17/2025
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
params:
  siblings_only: true
ms.reviewer: cchristenson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Android Intune settings catalog settings list

This article lists and describes the Android Enterprise settings you can configure in a settings catalog policy in Microsoft Intune. To learn more about the settings catalog, see [Settings catalog overview](settings-catalog.md).

This feature applies to:

- Android Enterprise corporate-owned devices with a work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)
- Android Open Source Project (AOSP) corporate-owned userless devices (shared)
- Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

## Before you begin

- At a minimum, sign into the Intune admin center as a member of the **Policy and Profile Manager** role. For more information on the built-in Intune roles, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).
- Create a [settings catalog policy](settings-catalog.md).

## Android settings

# [Android Enterprise](#tab/ae)

These settings apply to the Android Enterprise enrollment types where Intune controls the entire device, including the following enrollment types:

- Fully managed devices
- Dedicated devices
- Corporate-owned devices with a work profile

To learn more about the different Android enrollment types, see [Android Enrollment guide](../fundamentals/deployment-guide-enrollment-android.md).

### Device restriction

#### Device Password

  > [!NOTE]
  >
  > - Users on fully managed, and corporate-owned work profile devices aren't prompted to set a password. The settings are required, but users might not be notified. Users need to set the password manually. The policy reports as failed until the user sets a password that meets your requirements.
  >
  >   To apply the device password settings during device enrollment, assign the device restriction profile to users, not devices. During enrollment, users are asked to set a screen lock. Then, they must choose a device password that meets all the requirements in this device restriction profile.
  > - On dedicated devices, if the device is set up with single or multi-app kiosk mode, then users are prompted to set a password. Screens force and guide users to create a compliant password before they can continue using the device.
  > - On dedicated devices that aren't using kiosk mode, users aren't notified of any password requirement. Users need to set the password manually. The policy reports as failed until the user sets a password that meets your requirements.

- **Required password type**: Set the password's complexity requirements. More password requirements become available based on your selection.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Minimum password length**: Enter the minimum number of digits or characters the password must have, between 4 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of characters required**: Enter the number of characters the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of lowercase characters required**: Enter the number of lowercase characters the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of uppercase characters required**: Enter the number of uppercase characters the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of non-letter characters required**: Enter the number of non-letters (anything other than letters in the alphabet) the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of numeric characters required**: Enter the number of numeric characters (1, 2, 3, and so on) the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of symbol characters required**: Enter the number of symbol characters (&, #, %, and so on) the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of days until password expires**: Enter the number of days, until the device password must be changed, from 1-365. For example, enter 90 to expire the password after 90 days. When the password expires, users are prompted to create a new password. If the value is blank, Intune doesn't change or update this setting.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of passwords required before user can reuse a password**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter 5 so users can't set a new password to their current password or any of their previous four passwords. If the value is blank, Intune doesn't change or update this setting.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the device is wiped, from 4-11. If the value is blank, Intune doesn't change or update this setting.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Required unlock frequency**: Select how long users have before they're required to unlock the device using a strong authentication method (password, PIN, or pattern).

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Disable lock screen**: If **True**, this setting blocks all Keyguard lock screen features from being used. If **False**, Intune doesn't change or update this setting. By default, when the device is in lock screen, the OS might allow all the Keyguard features, such as camera, fingerprint unlock, and more.

  This feature applies to:

  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

#### General

- **Block Bluetooth**: If **True**, this setting disables Bluetooth on the device so that users can't pair with other devices. If **False**, Intune doesn't change or update this setting. By default, the OS might enable Bluetooth on the device.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

# [AOSP](#tab/aosp)

Android Open Source Project (AOSP) devices are Android devices that don't have Google Mobile Services (GMS) installed.

### Restrictions for AOSP devices

#### Device Password for AOSP devices

- **Required password type**: Set the password's complexity requirements. More password requirements become available based on your selection.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Minimum password length**: Enter the minimum number of digits or characters the password must have, between 4 and 16 characters.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the device is wiped, from 4-11. If the value is blank, Intune doesn't change or update this setting.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Maximum minutes of inactivity until screen locks**: Enter the maximum length of time, from 1 minute to 1 hour, that devices can be idle before the screen is automatically locked. Users must enter their credentials to regain access. For example, enter 5 to lock the device after 5 minutes of inactivity. Ignored by device if new time is longer than the time currently set on device. If set to Immediately, devices use the minimum possible value per device.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

#### General settings for AOSP devices

- **Block access to camera**: If **True**, this setting prevents access to the camera on the device. If **False**, Intune doesn't change or update this setting. By default, the OS might allow access to the camera. Intune only manages access to the device camera. It doesn't have access to pictures or videos.

  This feature applies to:

- Android Open Source Project (AOSP) corporate-owned userless devices (shared)
- Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Block screen capture**: If **True**, this setting prevents screenshots or screen captures on the device. It also prevents the content from being shown on display devices that don't have a secure video output. If **False**, Intune doesn't change or update this settingWhen set to Not configured (default), Intune doesn't change or update this setting. By default, the OS might let users capture the screen contents as an image.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Disable factory reset**: If **True**, this setting prevents users from using the factory reset option in the device's settings. If **False**, Intune doesn't change or update this setting. By default, the OS might allow external media on the device.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Block mounting of external media**: If **True**, this setting prevents users from using or connecting any external media on the device. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to connect external media.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)  

- **Block USB file transfer**: If **True**, this setting prevents users from transferring files over USB. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to transfer files.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Block Wi-Fi setting changes**: If **True**, this setting prevents users from creating or changing any Wi-Fi configurations. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to change the Wi-Fi settings on the device.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Block Bluetooth**: If **True**, this setting disables Bluetooth on the device so that users can't pair with other devices. If **False**, Intune doesn't change or update this setting. By default, the OS might enable Bluetooth on the device.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Block Bluetooth configuration**: If **True**, this setting prevents users from configuring Bluetooth on the device. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to configure Bluetooth.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Allow users to turn on debugging features**: If **True**, this setting permits users to access the debugging features on the device. If **False**, Intune doesn't change or update this setting. By default, the OS might prevent users from using the debugging features on the device.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

- **Block user from turning on unknown sources**: If **True**, this setting prevents users from sideloading apps. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to sideload apps from unknown sources.

  This feature applies to:

  - Android Open Source Project (AOSP) corporate-owned userless devices (shared)
  - Android Open Source Project (AOSP) corporate-owned user-associated devices (single user)

---

## Related articles

- [Settings catalog overview](settings-catalog.md)
- [Apple settings catalog](apple-settings-catalog-configurations.md)
