---
title: Android configuration list for Intune settings catalog
description: Use the Microsoft Intune settings catalog to add, configure, or restrict features on Android devices. This article lists and describes the settings you can configure.
author: MandiOhlinger
ms.author: mandia
ms.date: 09/15/2025
ms.topic: reference
params:
  siblings_only: true
ms.reviewer: cchristenson
ms.collection:
- M365-identity-device-management
---

# Android Intune settings catalog settings list

This article lists and describes the Android Enterprise and AOSP settings you can configure in a settings catalog policy in Microsoft Intune. To learn more about the settings catalog, see [Settings catalog overview](settings-catalog.md).

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

#### Applications

- **Allow installation from unknown sources**: If **True**, allows users to turn on Unknown sources. This setting allows apps to install from unknown sources, including sources other than the Google Play Store. It allows users to side-load apps on the device using means other than the Google Play Store. If **False**, Intune doesn't change or update this setting. By default, the OS might prevent users from turning on Unknown sources.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **App auto-updates (work profile-level)**: Select the auto update policy for apps. Your options:

  - **Not configured**: Intune doesn't change or update this setting.
  - **User choice**: End users can set their preference in managed Google Play.
  - **Never**: Apps never auto-update.
  - **Wi-Fi only**: Apps only auto-update when the device is connected to Wi-Fi.
  - **Always**: Apps always auto-update.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

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

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Minimum password length**: Enter the minimum number of digits or characters the password must have, between 4 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of characters required**: Enter the number of characters the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of lowercase characters required**: Enter the number of lowercase characters the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of uppercase characters required**: Enter the number of uppercase characters the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of non-letter characters required**: Enter the number of non-letters (anything other than letters in the alphabet) the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of numeric characters required**: Enter the number of numeric characters (1, 2, 3, and so on) the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of symbol characters required**: Enter the number of symbol characters (&, #, %, and so on) the password must have, between 0 and 16 characters.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of days until password expires**: Enter the number of days, until the device password must be changed, from 1-365. For example, enter 90 to expire the password after 90 days. When the password expires, users are prompted to create a new password. If the value is blank, Intune doesn't change or update this setting.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of passwords required before user can reuse a password**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter 5 so users can't set a new password to their current password or any of their previous four passwords. If the value is blank, Intune doesn't change or update this setting.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the device is wiped, from 4-11. If the value is blank, Intune doesn't change or update this setting.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Required unlock frequency**: Select how long users have before they're required to unlock the device using a strong authentication method (password, PIN, or pattern).

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Disable lock screen**: If **True**, this setting blocks all Keyguard lock screen features from being used. If **False**, Intune doesn't change or update this setting. By default, when the device is in lock screen, the OS might allow all the Keyguard features, like camera, fingerprint unlock, and more.

  This feature applies to:

  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

#### General

- **Allow access to developer settings**: If **True**, allow users access to the developer settings on the device. If **False**, Intune doesn't change or update this setting. By default, the OS might prevent users from accessing developer settings on the device.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block access to camera**: If **True**, prevents access to the camera on the device. If **False**, Intune doesn't change or update this setting. By default, the OS might allow access to the camera. Intune only manages access to the device camera. It doesn't have access to pictures or videos.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block beaming data from apps using NFC (work-profile level)**: If **True**, prevents using the Near Field Communication (NFC) technology to beam data from apps to other devices. If **False**, Intune doesn't change or update this setting. By default, the OS might allow using NFC to share data between devices.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

  This feature was deprecated in Android 10 and above. This setting can still be applied on newer devices, but it has no effect because the feature is no longer available.

- **Block Bluetooth**: If **True**, this setting disables Bluetooth on the device so that users can't pair with other devices. If **False**, Intune doesn't change or update this setting. By default, the OS might enable Bluetooth on the device.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block Bluetooth configuration**: If **True**, prevents users from configuring Bluetooth on the device. If **False**, Intune doesn't change or update this setting. By default, the OS might allow configuring Bluetooth on the device.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block factory reset**: If **True**, prevents users from using the factory reset option in the device settings. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to use this setting on the device

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block private space**: If **True**, users are prevented from creating or using private spaces on the device. All existing private spaces are deleted. If **False**, Intune doesn't change or update this setting. By default, the OS might allow private spaces.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)

- **Block roaming data services**: If **True**, prevents data roaming over the cellular network. If **False**, Intune doesn't change or update this setting. By default, the OS might allow data roaming when the device is on a cellular network.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block tethering and access to hotspots**: If **True**, prevents tethering and access to portable hotspots. If **False**, Intune doesn't change or update this setting. By default, the OS might allow tethering and access to portable hotspots.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block volume changes**: If **True**, prevents users from changing the device's volume, and also mutes the main volume. If **False**, Intune doesn't change or update this setting. By default, the OS might allow using the volume settings on the device.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

  This setting appears as successfully applied to COPE devices in reporting views, but it has no functional effect.

- **Block Wi-Fi access point configuration**: If **True**, prevents users from creating or changing any Wi-Fi configurations. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to change the Wi-Fi settings on the device.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Default permission policy**: Define the default permission policy for requests for runtime permissions. Your options:

  - Device default
  - Prompt
  - Auto grant
  - Auto deny

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Hide organization name**: If **True**, this setting prevents the enterprise name from being shown on the device, like on the lock screen. If **False**, Intune doesn't change or update this setting. By default, the OS might display the enterprise name.

  This feature applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)

- **USB access**: Select if files and/or data can be transferred using USB. Your options:

  - **Allow USB transfer**: All files and data are allowed to be transferred to and from USB. All USB connections are allowed, like a mouse.
  - **Disallow USB transfer**: Files are blocked from being transferred to and from USB. Other USB connections are allowed, like a mouse.
  - **Disallow USB data transfer**: All data is blocked to and from USB. No USB connections are allowed, like a mouse.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices at work profile level (COSU)

#### System Security

- **Require Common Criteria mode**: If **True**, enables an elevated set of security standards on the device most often used in highly sensitive organizations, like government establishments. If **False**, Intune doesn't change or update this setting.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

- **Require threat scan on apps**: If **True**, enables Google Play Protect to scan apps before and after they're installed. If it detects a threat, it might warn users to remove the app from the device. If **False**, Intune doesn't change or update this setting. By default, the OS might not enable or run Google Play Protect to scan apps.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE)
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

#### Users and Accounts

- **Block account changes**: If **True**, prevents users from updating or changing accounts when in kiosk mode. If **False**, Intune doesn't change or update this setting. By default, the OS might allow users to update user accounts on the device.

  Applies to:

  - Android Enterprise corporate owned dedicated devices (COSU)

- **Block users from configuring credentials (work profile-level)**: If **True**, prevents users from configuring certificates assigned to devices, even devices that aren't associated with a user account. If **False**, Intune doesn't change or update this setting. By default, the OS might make it possible for users to configure or change their credentials when they access them in the keystore.

  Applies to:

  - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
  - Android Enterprise corporate owned fully managed (COBO)
  - Android Enterprise corporate owned dedicated devices (COSU)

# [AOSP](#tab/aosp)

Android Open Source Project (AOSP) devices are Android devices that don't have Google Mobile Services (GMS) installed.

### Device restriction (AOSP)

#### Device Password (AOSP)

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

#### General (AOSP)

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
