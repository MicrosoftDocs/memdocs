---
# required metadata

title: Device restriction settings for Android in Microsoft Intune - Azure | Microsoft Docs
description: See a list of all the Android device settings you can control and restrict in Microsoft Intune. Use these settings to control the password, access Google Play, allow or prohibit apps, control the browser settings, block apps, backup to the Google cloud, and control the message, voice, data roaming, Wi-Fi, and Bluetooth connection options.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/19/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: ayesham, chrisbal
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Android and Samsung Knox Standard device restriction settings lists in Intune

This article shows you all the Microsoft Intune device restrictions settings that you can configure for devices running Android.

>[!TIP]
>If the settings you want are not available, you might be able to configure your devices using a [custom profile](../custom-settings-android.md).

## General

- **Camera**: Choose **Block** to prevent access to the camera. **Not configured** allows access to the device's camera.
- **Copy and paste (Samsung Knox only)**: Choose **Block** to prevent copy-and-paste. **Not configured** allows copy and paste functions on the device.
- **Clipboard sharing between apps (Samsung Knox only)**: Choose **Block** to prevent using the clipboard to copy-and-paste between apps. **Not configured** allows using the clipboard to copy and paste between apps.
- **Diagnostic data submission (Samsung Knox only)**: Choose **Block** to stop the user from submitting bug reports from the device. **Not configured** allows the user to submit the data.
- **Wipe (Samsung Knox only)**: Allows the user to run a [wipe](../remote-actions/devices-wipe.md) action on the device.
- **Geolocation (Samsung Knox only)**: Choose **Block** to disable the device from using location information. **Not configured** allows the device to use the location information.
- **Power off (Samsung Knox only)**: Choose **Block** to prevent the user from powering off device. If this setting is disabled, the **Number of sign-in failures before wiping device** setting can't be set, and doesn't work. **Not configured** allows the user to power off the device.
- **Screen capture (Samsung Knox only)**: Choose **Block** to prevent screenshots. **Not configured** lets the user capture the screen contents as an image.
- **Voice assistant (Samsung Knox only)**: Choose **Block** to disable the S Voice service. **Not configured** allows the use of S Voice service and app on the device. This setting doesn't apply to Bixby or the voice assistant for accessibility that reads the screen content aloud.
- **YouTube (Samsung Knox only)**: Choose **Block** to prevent users from using the YouTube app. **Not configured** allows using the YouTube app on the device.
- **Shared devices (Samsung Knox only)**: Configure a managed Samsung Knox Standard device as shared. When set to **Allow**, end users can sign in and out of the device with their Azure AD credentials. The device stays managed, whether it’s in use or not.</br>When used in with a SCEP certificate profile, this feature allows end users to share a device with the same apps for all users. But, each user has their own SCEP user certificate. When users sign out, all app data is cleared. This feature is limited to LOB apps only. </br>**Not configured** prevents multiple end users from signing in to the Company Portal app on the device using their Azure AD credentials.
- **Block date and time changes (Samsung Knox)**: Choose **Block** to prevent the user from changing the date and time settings on the device. **Not configured** allows users to change the date and time settings.

## Password

- **Password**: **Require** the end user to enter a password to access the device. **Not configured** allows users to access the device without entering a password.

    > [!NOTE]
    > Samsung Knox devices automatically require a 4-digit PIN during MDM enrollment. Native Android devices may automatically require a PIN to become compliant with Conditional Access.

- **Minimum password length**: Enter the minimum length of password a user must enter (between 4 and 16 characters).
- **Maximum minutes of inactivity until screen locks**: Enter the maximum number of minutes of inactivity allowed on the device until the screen locks. On a device, an end user can’t set a time value greater than the configured time in the profile. An end user can set a lower time value. For example, if the profile is set to 15 minutes, an end user can set the value to 5 minutes. An end user can’t set the value to 30 minutes. 
- **Number of sign-in failures before wiping device**: Enter the number of sign-in failures to allow before the device is wiped.
- **Password expiration (days)**: Enter the number of days before the device password must be changed.
- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default**
  - **Low security biometric**
  - **At least numeric**
  - **Numeric complex**: Repeated or consecutive numbers, such as "1111" or "1234", aren't allowed.<sup>1</sup>
  - **At least alphabetic**
  - **At least alphanumeric**
  - **At least alphanumeric with symbols**
- **Prevent reuse of previous passwords**: Stops the end user from creating a password they've used before.
- **Fingerprint unlock (Samsung Knox only)**: Choose **Block** to prevent using a fingerprint to unlock the device. **Not configured** allows the user to unlock the device using a fingerprint.
- **Smart Lock and other trust agents**: Choose **Block** to prevent Smart Lock or other trust agents from adjusting lock screen settings (Samsung KNOX Standard 5.0+). This phone feature, sometimes known as a trust agent, lets you disable or bypass the device lock screen password if the device is in a trusted location. For example, this feature can be used when the device is connected to a specific Bluetooth device, or when it's close to an NFC tag. You can use this setting to prevent users from configuring Smart Lock.
- **Encryption**: Choose **Require** so that files on the device are encrypted. Not all devices support encryption. To use this feature, also: 
  1. Set **Password** to **Require**.
  2. Set **Required password type** to **At least numeric**.
  3. Set **Minimum password length** to at least 4 to correctly report compliance for this setting.

  > [!NOTE]
  > If an encryption policy is enforced, Samsung Knox devices require users to set a 6-character complex password as the device passcode.

<sup>1</sup> Before you assign this setting to devices, be sure to update the Company Portal app to the latest version on those devices.

If you set **Required password type** to **Numeric complex**, and then assign it to a device running a version of Android earlier than 5.0, then following behavior applies:

- If the Company Portal app is running a version earlier than 1704, no PIN policy is applied to the device, and an error is shown in the Microsoft Endpoint Manager admin center.
- If the Company Portal app runs the 1704 version or later, only a simple PIN can be applied. Versions of Android earlier than 5.0 don't support this setting. No error is shown in the Microsoft Endpoint Manager admin center.

## Google Play Store

- **Google Play store (Samsung Knox only)**: Choose **Block** to prevent users from using the Google Play store. **Not configured** allows the user to access the Google Play store on the device.

## Restricted apps

Use these settings to allow or prevent specific apps on the device. This feature is supported on Android and Samsung Knox Standard devices:

- **Prohibited apps**: A list of apps not managed by Intune that you don't want installed on the device. If a user installs an app from this list, you're notified by Intune.
- **Approved apps**: A list of apps that users are allowed to install. To stay compliant, users must not install other apps. Apps that are managed by Intune are automatically allowed.

To add app to these lists, you can:

- **Add** the Google Play Store URL of the app you want. For example, to add the Microsoft Remote Desktop app for Android, enter `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`. To find the URL of an app, open the [Google Play store](https://play.google.com/store/apps), and search for the app. For example, search for `Microsoft Remote Desktop Play Store` or `Microsoft Planner`. Select the app, and copy the URL.
- Import a CSV file with details about the app, including the URL. Use the <*app url*>, <*app name*>, <*app publisher*> format. Or, **Export** an existing list that includes the restricted apps list in the same format.

> [!IMPORTANT]
> Device profiles that use the restricted app settings must be assigned to groups of users.

## Browser

- **Web browser (Samsung Knox only)**: Choose **Block** to prevent the default web browser from being used on the device. **Not configured** allows the device's default web browser to be used.
- **Autofill (Samsung Knox only)**: Choose **Block** to prevent the autofill of text in the browser. **Not configured** allows the autofill function of the web browser to be used.
- **Cookies (Samsung Knox only)**: Choose how you want to handle cookies from websites on the device. Your options:
  - Allow
  - Block all cookies
  - Allow cookies from visited web sites
  - Allow cookies from current web site
- **Javascript (Samsung Knox only)**: Choose **Block** to prevent the web browser from running Java scripts. **Not configured** allows the device web browser to run Java scripts.
- **Pop-ups (Samsung Knox only)**: Choose **Block** to prevent pop-ups in the web browser. **Not configured** allows pop-ups in the web browser.

## Allow or Block apps

Use these settings to allow, block, or hide specific apps on Samsung Knox Standard devices. Apps that are hidden can't be opened or ran by the user.

Your options:

- **Apps allowed to be installed (Samsung Knox Standard only)**
- **Apps blocked from launching (Samsung Knox Standard only)**
- **Apps hidden from user (Samsung Knox Standard only)**

For each setting, add a list of apps. Your options:

- **Add apps by package name**: Primarily used for line-of-business apps. Enter the app name, and the name of the app package.
- **Add apps by URL**: Enter the app name, and its URL in the Google Play store.
- **Add store app**: Select an app from the existing list of apps you manage in Intune.

## Cloud and Storage

- **Google backup (Samsung Knox only)**: Choose **Block** to prevent the device from syncing to Google backup. **Not configured** allows the use of Google backup.
- **Google account auto sync (Samsung Knox only)**: Choose **Block** to prevent the Google account auto sync feature on the device. **Not configured** allows Google account settings to be automatically synchronized.
- **Removable storage (Samsung Knox only)**: Choose **Block** to prevent the device from using removable storage. **Not configured** allows the device to use removable storage, like an SD card.
- **Encryption on storage cards (Samsung Knox only)**: **Require** enforces that storage cards must be encrypted. **Not configured** allows unencrypted storage cards to be used. Not all devices support storage card encryption. To confirm, check with the device manufacturer.

## Cellular and Connectivity

- **Data roaming (Samsung Knox only)**: Choose **Block** to prevent data roaming over the cellular network. **Not configured** allows data roaming when the device is on a cellular network.
- **SMS/MMS messaging (Samsung Knox only)**: Choose **Block** to prevent text messaging on the device. **Not configured** allows the use of SMS and MMS messaging on the device.
- **Voice dialing (Samsung Knox only)**: Choose **Block** to prevent users from using the voice dialing feature on the device. **Not configured** allows voice dialing on the device.
- **Voice roaming (Samsung Knox only)**: Choose **Block** to prevent voice roaming over the cellular network. **Not configured** allows voice roaming when the device is on a cellular network.
- **Bluetooth (Samsung Knox only)**: Choose **Block** to prevent using Bluetooth on the device. **Not configured** allows the use of Bluetooth on the device.
- **NFC (Samsung Knox only)**: Choose **Block** to stop the Near Field Communication (NFC) technology. **Not configured** allows operations that use near field communication on supported devices.
- **Wi-Fi (Samsung Knox only)**: Choose **Block** to prevent using Wi-Fi on the device. **Not configured** allows using the Wi-Fi features of the device.
- **Wi-Fi tethering (Samsung Knox only)**: Choose **Block** to prevent using Wi-Fi tethering on the device. **Not configured** allows the use of Wi-Fi tethering on the device.

## Kiosk

Kiosk settings apply only to Samsung Knox Standard devices, and only to apps you manage using Intune.

- Add apps you want to run when the device is in kiosk mode. In kiosk mode, only the apps you add run; apps not added don't run. Pre-installed browsers don't run as an app when the device is in kiosk mode. If a browser is required, consider using the [Managed Browser](../apps/app-configuration-managed-browser.md).

  Your app options:

  - **Add apps by package name**: Primarily used for line-of-business apps. Enter the app name, and the name of the app package.
  - **Add apps by URL**: Enter the app name, and its URL in the Google Play store.
  - **Add store app**: Select an app from the existing list of apps you manage in Intune.

- **Screen sleep button**: Choose **Block** to prevent or hide the screen sleep button. **Not configured** allows the screen sleep wake button on the device.
- **Volume buttons**: Choose **Block** to prevent the user from adjusting the volume by disabling the volume buttons. **Not configured** allows using the volume buttons on the device.

## Next steps

[Assign the profile](../device-profile-assign.md) and [monitor its status](../device-profile-monitor.md).

You can also create kiosk profiles for [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings) and [Windows 10](kiosk-settings.md) devices.
