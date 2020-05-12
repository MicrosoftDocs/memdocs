---
# required metadata

title: Device restriction settings for Android in Microsoft Intune - Azure | Microsoft Docs
description: See a list of all the Android device administrator settings you can control and restrict in Microsoft Intune. Use these settings to control the password, access Google Play, allow or prohibit apps, control the browser settings, block apps, backup to the Google cloud, and control the message, voice, data roaming, Wi-Fi, and Bluetooth connection options.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Android and Samsung Knox Standard device restriction settings lists in Intune

This article shows you all the Microsoft Intune device restrictions settings that you can configure for devices running Android.

>[!TIP]
>If the settings you want are not available, you might be able to configure your devices using a [custom profile](custom-settings-android.md).

## Before you begin

[Create a device configuration profile](device-restrictions-configure.md).

## General

- **Camera**: **Block** prevents access to the device camera. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the device camera.

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.

- **Copy and paste (Samsung Knox only)**: **Block** prevents copy-and-paste. **Not configured** allows copy and paste functions on devices.
- **Clipboard sharing between apps (Samsung Knox only)**: **Block** prevents using the clipboard to copy-and-paste between apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow copy and paste functions on devices.
- **Diagnostic data submission (Samsung Knox only)**: **Block** stops users from submitting bug reports from devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to submit the data.
- **Wipe (Samsung Knox only)**: Allows users to run a [wipe](../remote-actions/devices-wipe.md) action on devices. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Geolocation (Samsung Knox only)**: **Block** disables devices from using location information. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow devices to use the location information.
- **Power off (Samsung Knox only)**: **Block** prevents users from powering off device. It also prevents the **Number of sign-in failures before wiping device** setting from being configured, and from working. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to power off devices.
- **Screen capture (Samsung Knox only)**: **Block** prevents screenshots. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users capture the screen contents as an image.
- **Voice assistant (Samsung Knox only)**: **Block** disables the S Voice service. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the S Voice service and app on devices. This setting doesn't apply to Bixby or the voice assistant for accessibility that reads the screen content aloud.
- **YouTube (Samsung Knox only)**: **Block** prevents users from using the YouTube app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the YouTube app on devices.
- **Shared devices (Samsung Knox only)**: Configure a managed Samsung Knox Standard device as shared. **Allow** lets users sign in and out of devices with their Azure AD credentials. Devices stay managed, whether they're in use or not.

  When used in with a SCEP certificate profile, this feature allows users to share a device with the same apps for all users. But, each user has their own SCEP user certificate. When users sign out, all app data is cleared. This feature is limited to LOB apps only.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent multiple users from signing in to the Company Portal app on devices using their Azure AD credentials.
- **Block date and time changes (Samsung Knox)**: **Block** prevents users from changing the date and time settings on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the date and time settings.

## Password

- **Password**: **Require** users to enter a password to access devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access devices without entering a password.

    > [!NOTE]
    > Samsung Knox devices automatically require a 4-digit PIN during MDM enrollment. Native Android devices may automatically require a PIN to become compliant with Conditional Access.

- **Minimum password length**: Enter the minimum number of characters required, from 4-16. For example, enter `6` to require at least six numbers or characters in the password length.
- **Maximum minutes of inactivity until screen locks**: Enter the length of time a device must be idle before the screen is automatically locked. For example, enter `5` to lock devices after 5 minutes of being idle. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.

  On a device, users can't set a time value greater than the configured time in the profile. Users can set a lower time value. For example, if the profile is set to `15` minutes, users can set the value to 5 minutes. Users can't set the value to 30 minutes.

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before devices are wiped, from 4-11. `0` (zero) might disable device wipe functionality. When the value is blank, Intune doesn't change or update this setting.
- **Password expiration (days)**: Enter the number of days, until the device password must be changed, from 1-365. For example, enter `90` to expire the password after 90 days. When the password expires, users are prompted to create a new password. When the value is blank, Intune doesn't change or update this setting.
- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default**
  - **Low security biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **At least numeric**: Includes numeric characters, such as `123456789`.
  - **Numeric complex**: Repeated or consecutive numbers, such as "1111" or "1234", aren't allowed. Before you assign this setting to devices, be sure to update the Company Portal app to the latest version on those devices.

    When set to **Numeric complex**, and you assign the setting to devices running an Android version earlier than 5.0, then the following behavior applies:

    - If the Company Portal app is running a version earlier than 1704, no PIN policy applies to devices, and an error shows in the Microsoft Endpoint Manager admin center.
    - If the Company Portal app runs the 1704 version or later, only a simple PIN can be applied. Android version earlier than 5.0 don't support this setting. No error is shown in the Microsoft Endpoint Manager admin center.

  - **At least alphabetic**: Includes letters in the alphabet. Numbers and symbols aren't required.
  - **At least alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters.
  - **At least alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.

- **Prevent reuse of previous passwords**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Fingerprint unlock (Samsung Knox only)**: **Block** prevents using a fingerprint to unlock devices. When set to **Not configured** (default), Intune doesn't change or update this setting.By default, the OS might allow users to unlock devices using a fingerprint.
- **Smart Lock and other trust agents**: **Block** prevents Smart Lock or other trust agents from adjusting lock screen settings. If the device is in a trusted location, then this feature, also known as a trust agent, lets you disable or bypass the device lock screen password. For example, use this feature when devices are connected to a specific Bluetooth device, or when devices are close to an NFC tag. You can use this setting to prevent users from configuring Smart Lock.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

  This setting applies to:

  - Samsung KNOX Standard 5.0+

- **Encryption**: Choose **Require** so that files on the device are encrypted. Not all devices support encryption. When set to **Not configured** (default), Intune doesn't change or update this setting. To configure this setting, and correctly report compliance, also configure:
  1. **Password**: Set to **Require**.
  2. **Required password type**: Set to **At least numeric**.
  3. **Minimum password length**: Set to at least `4`.

  > [!NOTE]
  > If an encryption policy is enforced, Samsung Knox devices require users to set a 6-character complex password as the device passcode.

## Google Play Store

- **Google Play store (Samsung Knox only)**: **Block** prevents users from using the Google Play store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access the Google Play store on devices.

## Restricted apps

Use these settings to allow or prevent specific apps on devices. This feature is supported on Android and Samsung Knox Standard devices.

- **Not configured** (default): Intune doesn't change or update this 
setting.
- **Prohibited apps**: List the apps (not managed by Intune) that users aren't allowed to install and run. If a user installs an app from this list, you're notified by Intune.
- **Approved apps**: List the apps that users are allowed to install. To stay compliant, users must not install other apps.  Apps that are managed by Intune are automatically allowed, including the Company Portal app.
- **Apps list**: **Add** you app:
  - **App bundle ID**: Enter the app bundle ID.
  - **App store URL**: Enter the Google Play Store URL of the app you want. For example, to add the Microsoft Remote Desktop app for Android, enter `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`.

    To find the URL of an app, open the [Google Play store](https://play.google.com/store/apps), and search for the app. For example, search for `Microsoft Remote Desktop Play Store` or `Microsoft Planner`. Select the app, and copy the URL.
  
  - **App name**: Enter the name you want. This name is shown to users.
  - **Publisher** (optional): Enter the publisher of the app, such as `Microsoft`.

You can also **Import** a CSV file with details about the app, including the URL. Use the <*app url*>, <*app name*>, <*app publisher*> format. Or, **Export** an existing list that includes the restricted apps list in the same format.

> [!IMPORTANT]
> Device profiles that use the restricted app settings must be assigned to user groups, not device groups.

## Browser

- **Web browser (Samsung Knox only)**: **Block** prevents the default web browser from being used on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the device's default web browser to be used.
- **Autofill (Samsung Knox only)**: **Block** prevents the browser from automatically filling in text. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Autofill.
- **Cookies (Samsung Knox only)**: Choose how to handle cookies from websites on devices. Your options:
  - Allow
  - Block all cookies
  - Allow cookies from visited web sites
  - Allow cookies from current web site
- **JavaScript (Samsung Knox only)**: **Block** prevents JavaScript from running in the browser. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these scripts.
- **Pop-ups (Samsung Knox only)**: **Block** turns on Pop-up Blocker to prevent pop-ups in the web browser. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow pop-ups.

## Allow or Block apps

Use these settings to allow, block, or hide specific apps on Samsung Knox Standard devices. Apps that are hidden can't be opened or ran by users.

Your options:

- **Apps allowed to be installed (Samsung Knox Standard only)**: Add apps that users can install. Users can't install apps that aren't on the list.
- **Apps blocked from launching (Samsung Knox Standard only)**: Enter the apps that users can't run on their device.
- **Apps hidden from user (Samsung Knox Standard only)**: Enter the apps that are hidden on devices. Users can't discover or run these apps.

For each setting, add your apps:

- **Add apps by package name**: Enter the app name, and the name of the app package. Primarily used for line-of-business apps. 
- **Add apps by URL**: Enter the app name, and its URL in the Google Play store.
- **Add store app**: Select an app from the existing list of apps you manage in Intune.

## Cloud and Storage

- **Google backup (Samsung Knox only)**: **Block** prevents devices from syncing to Google backup. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using Google backup.
- **Google account auto sync (Samsung Knox only)**: **Block** prevents the Google account auto sync feature on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Google account settings to be automatically synchronized.
- **Removable storage (Samsung Knox only)**: **Block** prevents devices from using removable storage. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow devices to use removable storage, like an SD card.
- **Encryption on storage cards (Samsung Knox only)**: **Require** enforces that storage cards must be encrypted. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow unencrypted storage cards to be used. Not all devices support storage card encryption. To confirm, check with the device manufacturer.

## Cellular and Connectivity

- **Data roaming (Samsung Knox only)**: **Block** prevents data roaming over the cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow data roaming.
- **SMS/MMS messaging (Samsung Knox only)**: **Block** prevents text messaging on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using SMS and MMS messaging.
- **Voice dialing (Samsung Knox only)**: **Block** prevents users from using the voice dialing feature on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow voice dialing.
- **Voice roaming (Samsung Knox only)**: **Block** prevents voice roaming over the cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow voice roaming.
- **Bluetooth (Samsung Knox only)**: **Block** prevents using Bluetooth on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using Bluetooth.
- **NFC (Samsung Knox only)**: **Block** disables operations that use near field communication (NFC) on devices that support it. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow NFC operations.
- **Wi-Fi (Samsung Knox only)**: **Block** prevents using Wi-Fi on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using Wi-Fi.
- **Wi-Fi tethering (Samsung Knox only)**: **Block** prevents using Wi-Fi tethering on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using Wi-Fi tethering.

## Kiosk

Kiosk settings apply only to Samsung Knox Standard devices, and only to apps you manage using Intune.

- Add apps you want to run when the device is in kiosk mode. In kiosk mode, only the apps you add run; apps not added don't run. Pre-installed browsers don't run as an app when the device is in kiosk mode. If a browser is required, consider using the [Managed Browser](../apps/app-configuration-managed-browser.md).

  Your app options:

  - **Add apps by package name**: Primarily used for line-of-business apps. Enter the app name, and the name of the app package.
  - **Add apps by URL**: Enter the app name, and its URL in the Google Play store.
  - **Add store app**: Select an app from the existing list of apps you manage in Intune.

- **Screen sleep button**: **Block** prevents or hides the screen sleep button. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the screen sleep wake button on devices.
- **Volume buttons**: **Block** prevents users from adjusting the volume by disabling the volume buttons. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the volume buttons on devices.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also create kiosk profiles for [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) and [Windows 10](kiosk-settings.md) devices.
