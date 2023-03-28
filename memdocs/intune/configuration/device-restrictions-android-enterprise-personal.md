---
# required metadata

title: Personally owned Android Enterprise device restriction settings in Microsoft Intune
description: On Android Enterprise or Android for Work personally owned BYOD devices, you can restrict settings on the device using Microsoft Intune. Restrict copy and paste, notifications, app permissions, data sharing, password length, sign in failures, use fingerprint to unlock, reuse passwords, and enable bluetooth sharing of work contacts.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
# optional metadata

#ROBOTS:
#audience:

params:
  siblings_only: true
ms.reviewer: andreibiswas, shthilla, chmaguir, chrisbal, priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure, seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune

This article describes the different settings you can control on Android Enterprise devices. As part of your mobile device management (MDM) solution, use these settings to allow or disable features, control security, and more.

This feature applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

> [!TIP]
>
> - For **AOSP**, go to [Android (AOSP) device settings to allow or restrict features using Intune](device-restrictions-android-aosp.md).
> - For **Android Enterprise corporate-owned** work profile (COPE), fully managed (COBO), or dedicated devices (COSU), go to [Android Enterprise device settings to allow or restrict features on corporate-owned devices using Intune](device-restrictions-android-for-work.md).

## Before you begin

- Create an [Android device administrator device restrictions configuration profile](device-restrictions-configure.md).

- When you create device restriction policies, there are many settings available. To help determine the settings that are right for your organization, you can use the security configuration framework guidance:

  - [Android Enterprise personally owned work profile security settings](../enrollment/android-work-profile-security-settings.md)

## Work profile settings

These settings apply to Android Enterprise personally owned devices with a work profile (BYOD).

### General settings

- **Copy and paste between work and personal profiles**: **Block** prevents copy-and-paste between work and personal apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to share data using copy-and-paste with apps in the personal profile.
- **Data sharing between work and personal profiles**: Choose if apps in the work profile can share with apps in the personal profile. For example, you can control sharing actions within applications, such as the **Share…** option in the Chrome browser app. This setting doesn't apply to copy/paste clipboard behavior. Your options:
  - **Device default**: Sharing from the work profile to the personal profile is blocked. Sharing from the personal profile to the work profile is allowed.
  - **Apps in work profile can handle sharing request from personal profile**: Enables the built-in Android feature that allows sharing from the personal profile to the work profile. When enabled, a sharing request from an app in the personal profile can share with apps in the work profile. 
  - **No restrictions on sharing**: Enables sharing across the work profile boundary in both directions. When you select this setting, apps in the work profile can share data with unbadged apps in the personal profile. This setting allows managed apps in the work profile to share with apps on the unmanaged side of the device. So, use this setting carefully.

- **Work profile notifications while device locked**: **Block** prevents window notifications, including toasts, incoming calls, outgoing calls, system alerts, and system errors from showing on locked devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show notifications.
- **Default app permissions**: Sets the default permission policy for all apps in the work profile. Starting with Android 6, users are prompted to grant certain permissions required by apps when the app is launched. This policy setting lets you decide if users are prompted to grant permissions for all apps in the work profile. For example, you assign an app to the work profile that requires location access. Normally that app prompts users to approve or deny location access to the app. Use this policy to automatically grant permissions without a prompt, automatically deny permissions without a prompt, or let users decide. Your options:
  - **Device default**
  - **Prompt**
  - **Auto grant**
  - **Auto deny**

  You can also use an app configuration policy to grant permissions for individual apps (**Apps** > **App configuration policies**).

- **Add and remove accounts**: This setting allows or prevents accounts from being added in the work profile, including Google accounts. Your options:

  - **Block all account types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.
  - **Allow all account types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**.

    This setting requires:

    - Google Play app version 80970100 or higher

  - **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

    In a previous release, this setting was named **Not configured**.

  > [!NOTE]
  >
  > - On corporate owned devices with work profile (COPE), Google accounts can't be added to the **Settings** app > **Accounts** > **Work**.
  > - This setting uses the [Restrict accounts in Google Play](https://developer.android.com/work/dpc/security#google-play-accounts) feature (opens Android's web site).

- **Contact sharing via Bluetooth**: **Enable** allows sharing and access to personally owned devices with a work profile contacts from another device, including a car, that's paired using Bluetooth. Enabling this setting may allow certain Bluetooth devices to cache work contacts upon first connection. Disabling this policy after an initial pairing/sync may not remove work contacts from a Bluetooth device.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not share work contacts.

  This setting applies to:

  - Android 8.0 and newer personally owned devices with a work profile

- **Screen capture**: **Block** prevents screenshots or screen captures on the device in the work profile. It also prevents the content from being shown on display devices that don't have a secure video output. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow getting screenshots.

- **Display work contact caller-id in personal profile**: **Block** doesn't show the work contact caller number in the personal profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show work contact caller details.

  This setting applies to:

  - Android 8.0 and newer personally owned devices with a work profile

- **Search work contacts from personal profile**: **Block** prevents users from searching for work contacts in apps in the personal profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow searching for work contacts in the personal profile.

- **Camera**: **Block** prevents access to the camera on the device in the personally owned work profile. This setting doesn't affect the camera on the personal side. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the camera.

- **Allow widgets from work profile apps**: **Enable** allows users to put widgets exposed by apps on the home screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable this feature.

  For example, Outlook is installed on your users' work profile. When set to **Enable**, users can put the agenda widget on the device home screen.

### Work Profile Password

These password settings apply to the work profile password on personally owned devices with a work profile.

#### All Android devices

- **Require Work Profile Password**: **Require** forces a passcode policy that only applies to apps in the work profile. By default, users can use the two separately defined PINs. Or, users can combine the PINs into the stronger of the two PINs. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use work apps without entering a password.

  This setting applies to:

  - Android 8.0 and newer personally owned devices with a work profile

- **Maximum minutes of inactivity until work profile locks**: Enter the length of time devices must be idle before the screen is automatically locked. Users must enter their credentials to regain access. For example, enter `5` to lock the device after 5 minutes of being idle. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.

  On devices, users can't set a time value greater than the configured time in the profile. Users can set a lower time value. For example, if the profile is set to `15` minutes, users can set the value to 5 minutes. Users can't set the value to 30 minutes.

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the work profile on the device is wiped, from 4-11. `0` (zero) might disable the device wipe functionality. When the value is blank, Intune doesn't change or update this setting.

- **Password expiration (days)**: Enter the number of days until user passwords must be changed (from **1**-**365**).

- **Prevent reuse of previous passwords**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Face unlock**: **Block** prevents users from using the device's facial recognition to unlock the personally owned work profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using facial recognition.
- **Fingerprint unlock**: **Block** prevents users from using the device's fingerprint scanner to unlock the personally owned work profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using a fingerprint.
- **Iris unlock**: **Block** prevents users from using the device's iris scanner to unlock the personally owned work profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using the iris scanner.
- **Smart Lock and other trust agents**: **Block** prevents Smart Lock or other trust agents from adjusting lock screen settings on compatible devices. If devices are in a trusted location, then this feature, also known as a trust agent, lets you disable or bypass the device lock screen password. For example, bypass the work profile password when devices are connected to a specific Bluetooth device, or when devices are close to an NFC tag. Use this setting to prevent users from configuring Smart Lock.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

#### Android 12 and later

- **Password complexity**: Use this setting to set the password complexity requirements. Your options:

  - **None**: Intune doesn't change or update this setting. By default, the OS may not require a password.
  - **Low**: A pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are allowed.
  - **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least 4 characters.
  - **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters.

  On personally owned devices with a work profile, there are two passwords affected by this **Password complexity** setting:

  - The device password that unlocks the device
  - The work profile password that allows users to access the work profile

  If the device password complexity is too low, then the device password is automatically changed to require a **High** complexity. The end users must update the device password to meet the complexity requirements. Then, they sign into the work profile and are prompted to update the work profile complexity configured in the **Password complexity** setting in your policy.  

  > [!IMPORTANT]
  >
  > Before the **Password complexity** setting was available, the **Required password type** and **Minimum password length** settings were used. These settings are still available, but they're deprecated by Google for Android 12+ personally owned devices with a work profile. For information on these settings, go to [Android 11 and earlier](#android-11-and-earlier) (in this article).
  >
  > Here's what you need to know:
  >
  > - If the **Required password type** and **Minimum password length** settings are changed from the default values in a policy, then:
  >   - Newly enrolled Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity. So if you don't want a **High** password complexity, then create a new policy for Android Enterprise 12+ devices and configure the **Password complexity** setting.
  >   - Existing Android Enterprise 12+ devices will continue to use the **Required password type** and **Minimum password length** settings, and the existing values that are already configured.
  >
  >     If you change an existing policy with the **Required password type** and **Minimum password length** settings that already configured, then Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity.
  >
  >     For Android Enterprise 12+ devices, it's recommended to configure the **Password complexity** setting.
  > 
  > - If the **Required password type** and **Minimum password length** settings aren't changed from the default values in a policy, then no password policy is automatically applied to newly enrolled Android Enterprise 12+ devices.

#### Android 11 and earlier

> [!IMPORTANT]
> 
> - Google is deprecating these **Required password type** and **Minimum password length** settings for Android 12+ personally owned devices with a work profile and replacing it with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).
  > - On Android Enterprise 12+ devices, use the **Password complexity** setting.

- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default** (default): Intune doesn't change or update this setting. By default, the OS might not require a password.
  - **Low security biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **Required**
  - **At least numeric**: Includes numeric characters, such as `123456789`.
  - **Numeric complex**: Repeated or consecutive numbers, such as `1111` or `1234`, aren't allowed.
  - **At least alphabetic**: Includes letters in the alphabet. Numbers and symbols aren't required.
  - **At least alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters.
  - **At least alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.

- **Minimum password length**: Enter the minimum length the password must have, between 4 (default) and 16 characters.

## Password

These password settings apply to the device password on personally owned devices with a work profile.

### All Android devices

- **Maximum minutes of inactivity until screen locks**: Enter the length of time devices must be idle before the screen is automatically locked. Users must enter their credentials to regain access. For example, enter `5` to lock the device after 5 minutes of being idle. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.

  On devices, users can't set a time value greater than the configured time in the profile. Users can set a lower time value. For example, if the profile is set to `15` minutes, users can set the value to 5 minutes. Users can't set the value to 30 minutes.

- **Number of sign-in failures before wiping device**: Enter the number of wrong passwords allowed before the personally owned work profile in the device is wiped, from 4-11. `0` (zero) might disable the device wipe functionality. When the value is blank, Intune doesn't change or update this setting.
- **Password expiration (days)**: Enter the number of days, until the device password must be changed, from 1-365. For example, enter `90` to expire the password after 90 days. When the password expires, users are prompted to create a new password. When the value is blank, Intune doesn't change or update this setting.

- **Prevent reuse of previous passwords**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter `5` so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Fingerprint unlock**: **Block** prevents users from using the device's fingerprint scanner to unlock the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using a fingerprint.
- **Face unlock**: **Block** prevents users from using the device's facial recognition to unlock the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using facial recognition.
- **Iris unlock**: **Block** prevents users from using the device's iris scanner to unlock the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using the iris scanner.
- **Smart Lock and other trust agents**: **Block** prevents Smart Lock or other trust agents from adjusting lock screen settings on compatible devices. If devices are in a trusted location, then this feature, also known as a trust agent, lets you disable or bypass the device lock screen password. For example, bypass the personally owned work profile password when devices are connected to a specific Bluetooth device, or when devices are close to an NFC tag. Use this setting to prevent users from configuring Smart Lock.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

### Android 12 and later

- **Password complexity**: Use this setting to set the password complexity requirements. Your options:

  - **None**: Intune doesn't change or update this setting. By default, the OS may not require a password.
  - **Low**: A pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are allowed.
  - **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least 4 characters.
  - **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters.

  On personally owned devices with a work profile, there are two passwords affected by this **Password complexity** setting:

  - The device password that unlocks the device
  - The work profile password that allows users to access the work profile

  If the device password complexity is too low, then the device password is automatically changed to require a **High** complexity. The end users must update the device password to meet the complexity requirements. Then, they sign into the work profile and are prompted to update the work profile complexity configured in the **Password complexity** setting in your policy.

  > [!IMPORTANT]
  >
  > Before the **Password complexity** setting was available, the **Required password type** and **Minimum password length** settings were used. These settings are still available, but they're deprecated by Google for Android 12+ personally owned devices with a work profile. For more information on these settings, go to [Android 11 and earlier](#android-11-and-earlier-1) (in this article).
  >
  > Here's what you need to know:
  >
  > - If the **Required password type** and **Minimum password length** settings are changed from the default values in a policy, then:
  >   - Newly enrolled Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity. So if you don't want a **High** password complexity, then create a new policy for Android Enterprise 12+ devices and configure the **Password complexity** setting.
  >   - Existing Android Enterprise 12+ devices will continue to use the **Required password type** and **Minimum password length** settings, and the existing values that are already configured.
  >
  >     If you change an existing policy with the **Required password type** and **Minimum password length** settings that already configured, then Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity.
  >
  >     For Android Enterprise 12+ devices, it's recommended to configure the **Password complexity** setting.
  > 
  > - If the **Required password type** and **Minimum password length** settings aren't changed from the default values in a policy, then no password policy is automatically applied to newly enrolled Android Enterprise 12+ devices.

### Android 11 and earlier

> [!IMPORTANT]
> 
> - Google is deprecating these **Required password type** and **Minimum password length** settings for Android 12+ personally owned devices with a work profile and replacing it with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).
  > - On Android Enterprise 12+ devices, use the **Password complexity** setting.

- **Required password type**: Enter the required password complexity level, and whether biometric devices can be used. Your options:
  - **Device default** (default): Intune doesn't change or update this setting. By default, the OS might not require a password.
  - **Low security biometric**: [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **Required**
  - **At least numeric**: Includes numeric characters, such as `123456789`.
  - **Numeric complex**: Repeated or consecutive numbers, such as `1111` or `1234`, aren't allowed.
  - **At least alphabetic**: Includes letters in the alphabet. Numbers and symbols aren't required.
  - **At least alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters.
  - **At least alphanumeric with symbols**: Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.

- **Minimum password length**: Enter the minimum length the password must have, between 4 (default) and 16 characters.

## System security

- **Threat scan on apps**: **Require** enforces that the **Verify Apps** setting is enabled for work and personal profiles. When set to **Not configured** (default), Intune doesn't change or update this setting.

  This setting applies to:

  - Android 8 (Oreo) and newer personally owned devices with a work profile

- **Prevent app installations from unknown sources in the personal profile**: By design, Android Enterprise personally owned devices with a work profile can't install apps from sources other than the Play Store. This setting allows administrators more control of app installations from unknown sources. **Block** prevents app installations from sources other than the Google Play Store in the personal profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow app installations from unknown sources in the personal profile. By nature, personally owned devices with a work profile are intended to be dual-profile:

  - A personally owned device with a work profile managed using MDM.
  - A personal profile that's isolated from MDM management.

## Connectivity

- **Always-on VPN**: **Enable** sets a VPN client to automatically connect and reconnect to the VPN. Always-on VPN connections stay connected. Or, immediately connect when users lock their device, the device restarts, or the wireless network changes.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable always-on VPN for all VPN clients.

  > [!IMPORTANT]
  > Be sure to deploy only one Always On VPN policy to a single device. Deploying multiple Always VPN policies to a single device isn't supported.

- **VPN client**: Choose a VPN client that supports Always On. Your options:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Custom
    - **Package ID**: Enter the package ID of the app in the Google Play store. For example, if the URL for the app in the Play store is `https://play.google.com/store/details?id=com.contosovpn.android.prod`, then the package ID is `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  >
  > - The VPN client you choose must be installed on the device. It must also support per-app VPN in personally owned devices with a work profile. Otherwise, an error occurs.
  > - You do need to approve the VPN client app in the **Managed Google Play Store**, sync the app to Intune, and deploy the app to the device. After you do this, then the app is installed in the user's personally owned devices with a work profile.
  > - There may be known issues when using per-app VPN with F5 Access for Android 3.0.4. For more information, see [F5's release notes for F5 Access for Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Lockdown mode**: **Enable** forces all network traffic to use the VPN tunnel. If a connection to the VPN isn't established, then the device won't have network access.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow traffic to flow through the VPN tunnel or through the mobile network.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

[Configure and troubleshoot Android enterprise devices in Microsoft Intune](https://support.microsoft.com/help/4476974).
