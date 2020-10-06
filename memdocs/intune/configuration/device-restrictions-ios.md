---
# required metadata
title: iOS/iPadOS device settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add, configure, or create settings on iOS/iPadOS devices to restrict features in Microsoft Intune. Create password requirements, control the locked screen, use built-in apps, add restricted or approved apps, handle bluetooth devices, connect to the cloud for backup and storage, enable kiosk mode, add domains, and control how users interact with the Safari web browser.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
---

# iOS and iPadOS device settings to allow or restrict features using Intune

This article lists and describes the different settings you can control on iOS and iPadOS devices. As part of your mobile device management (MDM) solution, use these settings to allow or disable features, set password rules, allow or restrict specific apps, and more.

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your iOS/iPadOS devices.

> [!TIP]
> These settings use Apple's MDM settings. For more information on these settings, see [Apple's mobile device management settings](https://support.apple.com/guide/mdm/welcome/web) (opens Apple's web site).

## Before you begin

Create an [iOS/iPadOS device restrictions configuration profile](device-restrictions-configure.md).

> [!NOTE]
> These settings apply to different enrollment types, with some settings applying to all enrollment options. For more information on the different enrollment types, see [iOS/iPadOS enrollment](../enrollment/ios-enroll.md).

## General

### Settings apply to: All enrollment types

- **Share usage data**: **Block** prevents devices from sending diagnostic and usage data to Apple. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this data to be sent.

- **Screen capture**: **Block** prevents screenshots or screen captures on devices. In iOS/iPadOS 9.0 and newer, it also blocks screen recordings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users capture the screen contents as an image or as a video.

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Untrusted TLS certificates**: **Block** prevents untrusted Transport Layer Security (TLS) certificates on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow TLS certificates.
- **Block over-the-air PKI updates**: **Block** prevents your users from receiving software updates unless devices are connected to a computer. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow a device to receive software updates without being connected to a computer.
- **Limit ad tracking**: **Limit** disables the device advertising identifier. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might keep it enabled.
- **Enterprise app trust**: **Block** removes the **Trust Enterprise Developer** button in Settings > General > Profiles & Device Management on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users choose to trust apps that aren't downloaded from the app store.
- **Block App Clips**: **Yes** blocks App Clips on managed devices. Specifically, setting to **Yes**:

  - Prevents users from adding App Clips on devices.
  - Removes existing App Clips on devices.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow adding and removing App Clips on devices.

  This feature applies to:  
  - iOS 14.0 and newer
  - iPadOS 14.0 and newer

### Settings apply to: Automated device enrollment (supervised)

- **Diagnostics submission settings modification**: **Block** prevents users from changing the diagnostic submission and app analytics settings in **Diagnostics and Usage** (device Settings). When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change these device settings.

  To use this setting, set the **Share usage data** setting to **Block**.

  This feature applies to:  
  - iOS 9.3.2 and newer
  - iPadOS 13.0 and newer

- **Remote screen observation by Classroom app**: **Block** prevents the Classroom app from remotely viewing the screen on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the Apple Classroom app to view the screen.

  To use this setting, set the **Screen capture** setting to **Block**.

  This feature applies to:  
  - iOS 9.3 - iOS 12.x: Requires supervised devices
  - iOS 13.0 and newer: Doesn't require supervised devices
  - iPadOS 13.0 and newer: Devices must be enrolled using Device Enrollment or Automated Device Enrollment (ADE)

- **Unprompted screen observation by Classroom app**: **Allow** lets teachers silently observe students' iOS/iPadOS screens using the Classroom app without the students knowing. Student devices enrolled in a class using the Classroom app automatically give permission to that course's teacher. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent this feature.

  To use this setting, set the **Screen capture** setting to **Block**.

- **Account modification**: **Block** prevents users from updating device-specific settings from the iOS/iPadOS settings app. For example, users can't create new device accounts, or change the user name or password. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change these settings.

  This feature also applies to settings accessible from the iOS/iPadOS settings app, such as Mail, Contacts, Calendar, Twitter, and more. This feature doesn't apply to apps with account settings that aren't configurable from the iOS/iPadOS settings app, such as the Microsoft Outlook app.

- **Screen time**: **Block** prevents users from setting their own restrictions in Screen Time (device settings). When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to configure device restrictions (such as parental controls or content, and privacy restrictions) on devices.

  This setting was renamed from **Enabling restrictions in the device settings**. Impact of this change:  
  
  - iOS 11.4.1 and older: **Block** prevents users from setting their own restrictions in the device settings. The behavior is the same; and there are no changes for users.
  - iOS 12.0 and newer: **Block** prevents users from setting their own **Screen Time** in the device settings (Settings > General > Screen Time), including content and privacy restrictions. Devices upgraded to iOS 12.0 won't see the restrictions tab in the device settings anymore (Settings > General > Device Management > Management Profile > Restrictions). These settings are in **Screen Time**.
  
- **Use of the erase all content and settings option on the device**: **Block** prevents using the erase all content and settings option on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might give users access to these settings.
- **Device name modification**: **Block** prevents changing the device name. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the name of devices.
- **Notification settings modification**: **Block** prevents changing the notification settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the device notification settings.
- **Wallpaper modification**: **Block** prevents the wallpaper from being changed. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the wallpaper on devices.
- **Configuration profile changes**: **Block** prevents configuration profile changes on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to install configuration profiles.
- **Activation Lock**: **Allow** enables Activation Lock on supervised iOS/iPadOS devices. Activation Lock makes it harder for a lost or stolen device to be reactivated. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Block app removal**: **Block** prevents removing apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to remove apps from devices.
- **Allow USB accessories while device is locked**: **Allow** lets USB accessories exchange data with devices that are locked for over an hour. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not update USB Restricted mode on devices, and USB accessories are blocked from transferring data from devices if locked for over an hour.

  This feature applies to:  
  - iOS/iPadOS 11.4.1 and newer

- **Force automatic date and time**: **Require** forces supervised devices to set the Date & Time automatically. The device's time zone is updated when the device has cellular connections or has Wi-Fi with location services enabled. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Require students to request permission to leave Classroom course**: **Require** forces students enrolled in an unmanaged course using the Classroom app to request permission from the teacher to leave the course. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not force the student to ask for permission.

  This feature applies to:  
  - iOS 11.3 and newer
  - iPadOS 13.0 and newer

- **Allow Classroom to lock to an app and lock the device without prompting**: **Enable** allows teacher to lock apps or lock devices using the Classroom app without prompting the student. Locking apps means devices can only access teacher specified apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent teachers from locking apps or devices using the Classroom app without prompting the student.

  This feature applies to:  
  - iOS 11.0 and newer
  - iPadOS 13.0 and newer

- **Automatically join Classroom classes without prompting**: **Enable** automatically allows students to join a class that's in the Classroom app without prompting the teacher. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prompt the teacher that students want to join a class that's in the Classroom app.

  This feature applies to:  
  - iOS 11.0 and newer
  - iPadOS 13.0 and newer

- **Block VPN creation**: **Block** prevents users from creating VPN configuration settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users create VPNs on devices.
- **Modifying eSIM settings**: **Block** prevents removing or adding a cellular plan to the eSIM on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change these settings.

  This feature applies to:  
  - iOS 12.1 and newer
  - iPadOS 13.0 and newer

- **Defer software updates**: **Enable** allows you to delay when software updates are shown on devices, from 0-90 days. This setting doesn't control when updates are or aren't installed.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show software updates on devices as Apple releases them. For example, if an iOS/iPadOS update gets released by Apple on a specific date, then that update naturally shows up on devices around the release date.  

  - **Delay visibility of software updates**: Enter a value from 0-90 days. When the delay expires, users get notified to update to the earliest OS version available when the delay is triggered.

    For example, if iOS 12.a is available on **January 1**, and **Delay visibility** is set to **5 days**, then iOS 12.a isn't shown as an available update on user devices. On the **sixth day** following the release, that update is available, and users can install it.

    This feature applies to:  
    - iOS 11.3 and newer
    - iPadOS 13.0 and newer

## Password

### Settings apply to: All enrollment types

- **Password**: **Require** users to enter a password to access devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access devices without entering a password.

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

> [!IMPORTANT]
> On user-enrolled devices, if you configure any password setting, then the **Simple passwords** settings is automatically set to **Block**, and a 6 digit PIN is enforced.
>
> For example, you configure the **Password expiration** setting, and push this policy to user-enrolled devices. On the devices, the following happens:
>
> - The **Password expiration** setting is ignored.
> - Simple passwords, such as `1111` or `1234`, aren't allowed.
> - A 6 digit pin is enforced.

- **Simple passwords**: **Block** requires more complex passwords. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow simple passwords, such as `0000` and `1234`.

- **Required password type**: Enter the required password complexity level your organization requires. Your options:
  - **Device default**
  - **Numeric**: Password must only be numbers, such as 123456789.
  - **Alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters.

  > [!NOTE]
  > Selecting alphanumeric can impact a paired Apple Watch. For more information, see [Set passcode restrictions for an Apple Watch](https://support.apple.com/HT204953) (opens Apple's web site).

- **Number of non-alphanumeric characters in password**: Enter the number of symbol characters, such as `#` or `@`, that must be included in the password, from 1-4. When set to **Not configured** (default), Intune doesn't change or update this setting.

- **Minimum password length**: Enter the minimum length the password must have, from 4-16 characters. On user enrolled devices, enter a length between 4 and 6 characters.
  
  > [!NOTE]
  > For devices that are user enrolled, users can set a PIN greater than 6 digits. But, no more than 6 digits are enforced on devices. For example, an administrator sets the minimum length to `8`. On user-enrolled devices, users are only required to set a 6 digit PIN. Intune doesn't force a PIN greater than 6 digits on user-enrolled devices.

- **Number of sign-in failures before wiping device**: Enter the number of failed sign-ins before the device is wiped, from 2-11. It's not recommended to set this value to `2` or `3`. It's very common to enter the wrong password. Wiping the device after two or three incorrect password attempts happens often. It's recommended to set this value to at least `4`. 
  
  iOS/iPadOS has built-in security that can impact this setting. For example, iOS/iPadOS may delay triggering the policy depending on the number of sign in failures. It may also consider repeatedly entering the same passcode as one attempt. Apple's [iOS/iPadOS security guide](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) (opens Apple's web site) is a good resource, and provides more specific details on passcodes. 
  
- **Maximum minutes after screen lock before password is required**<sup>1</sup>: Enter how long devices stay idle before users must reenter their password. If the time you enter is longer than what's currently set on the device, then the device ignores the time you enter.

  This feature applies to:  
  - iOS 8.0+
  - iPadOS 13.0+

- **Maximum minutes of inactivity until screen locks**<sup>1</sup>: Enter the maximum number of minutes of inactivity allowed on devices until the screen locks.

  **iOS/iPadOS options**:  

  - **Not configured** (Default): Intune doesn't change or update this setting.
  - **Immediately**: Screen locks after 30 seconds of inactivity.
  - **1**: Screen locks after 1 minute of inactivity.
  - **2**: Screen locks after 2 minutes of inactivity.
  - **3**: Screen locks after 3 minutes of inactivity.
  - **4**: Screen locks after 4 minutes of inactivity.
  - **5**: Screen locks after 5 minutes of inactivity.

  **iPadOS options**:  

  - **Not configured** (Default): Intune doesn't change or update this setting.
  - **Immediately**: Screen locks after 2 minutes of inactivity.
  - **2**: Screen locks after 2 minutes of inactivity.
  - **5**: Screen locks after 5 minutes of inactivity.
  - **10**: Screen locks after 10 minutes of inactivity.
  - **15**: Screen locks after 15 minutes of inactivity.

  If a value doesn't apply to iOS and iPadOS, then Apple uses the closest *lowest* value. For example, if you enter `4` minutes, then iPadOS devices use `2` minutes. If you enter `10` minutes, then iOS devices use `5` minutes. This behavior is an Apple limitation.
  
  > [!NOTE]
  > The Intune UI for this setting doesn't separate the iOS and iPadOS supported values. The UI might be updated in a future release.

- **Password expiration (days)**: Enter the number of days before the device password must be changed, from 1-65535.
- **Prevent reuse of previous passwords**: Use this setting to restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter 5 so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
- **Touch ID and Face ID unlock**: **Block** prevents using a fingerprint or face to unlock devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock devices using biometrics.

  Blocking this setting also prevents using FaceID authentication to unlock devices.

  Face ID applies to:  
  - iOS 11.0 and newer
  - iPadOS 13.0 and newer

### Settings apply to: Automated device enrollment (supervised)

- **Passcode modification**: **Block** stops the passcode from being changed, added, or removed. After blocking this feature, changes to passcode restrictions are ignored on supervised devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passcodes to be added, changed, or removed.

  - **Touch ID and Face ID modification**: **Block** stops users from changing, adding, or removing TouchID fingerprints and Face ID. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to update the TouchID fingerprints and Face ID on devices.

    Blocking this setting also stops users from changing, adding, or removing FaceID authentication.

    Face ID applies to:  
    - iOS 11.0 and newer
    - iPadOS 13.0 and newer

- **Block password AutoFill**: **Block** prevents using the AutoFill Passwords feature on iOS/iPadOS. Choosing **Block** also has the following impact:

  - Users aren't prompted to use a saved password in Safari or in any apps.
  - Automatic Strong Passwords are disabled, and strong passwords aren't suggested to users.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these features.

- **Block password proximity requests**: **Block** prevents devices from requesting passwords from nearby devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these password requests.
- **Block password sharing**: **Block** prevents sharing passwords between devices using AirDrop. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passwords to be shared.
- **Require Touch ID or Face ID authentication for password or credit card information AutoFill**: **Require** forces users to authenticate using TouchID or FaceID before passwords or credit card information can be auto filled in Safari and other apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to control this feature in the device settings.

  This feature applies to:  
  - iOS 11.0 and newer
  - iPadOS 13.0 and newer
  
<sup>1</sup> When you configure the **Maximum minutes of inactivity until screen locks** and **Maximum minutes after screen lock before password is required** settings, they're applied in sequence. For example, if you set the value for both settings to **5** minutes, the screen turns off automatically after five minutes, and devices are locked after an additional five minutes. However, if users turn off the screen manually, the second setting is immediately applied. In the same example, after users turn off the screen, the device locks five minutes later.

## Locked Screen Experience

### Settings apply to: All enrollment types

- **Control Center access while device locked**: **Block** prevents access to the Control Center app while device is locked. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the Control Center app when devices are locked.
- **Notifications while device locked**: **Block** prevents access to notifications when devices are locked. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to notifications without unlocking devices.
- **Today view while device locked**: **Block** prevents access to the Today view when devices are locked. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to see the Today view when devices are locked.

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Wallet notifications while device locked**: **Block** prevents access to the Wallet app when devices are locked. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the Wallet app while devices are locked.

## App Store, Doc Viewing, Gaming

### Settings apply to: All enrollment types

- **Viewing corporate documents in unmanaged apps**: **Block** prevents viewing corporate documents in unmanaged apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow corporate documents to be viewed in any app.

  For example, you want to prevent users from saving files from the OneDrive app to Dropbox. Configure this setting as **Block**. After devices receive the policy (for example, after a restart), it no longer allows saving.

  > [!NOTE]
  > When this setting is blocked, third party keyboards installed from the App Store are also blocked.

  - **Allow unmanaged apps to read from managed contacts accounts**: **Allow** lets unmanaged apps, such as the built-in iOS/iPadOS Contacts app, to read and access contact information from managed apps, including the Outlook mobile app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent reading, including removing duplicates, from the built-in Contacts app on devices.  
  
    This setting allows or prevents reading contact information. It doesn't control syncing contacts between the apps.
  
    To use this setting, set the **Viewing corporate documents in unmanaged apps** setting to **Block**.

  For more information about these two settings, and their impact on Outlook for iOS/iPadOS contact export synchronization, see [Support Tip: Use Intune custom profile settings with the iOS/iPadOS Native Contacts App](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **Treat AirDrop as an unmanaged destination**: **Require** forces AirDrop to be considered an unmanaged drop target. It stops managed apps from sending data using Airdrop. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Viewing non-corporate documents in corporate apps**: **Block** prevents viewing non-corporate documents in corporate apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow any document to be viewed in corporate managed apps.

  **Block** also prevents contact export synchronization in Outlook for iOS/iPadOS. For more information, see [Support Tip: Enabling Outlook iOS/iPadOS Contact Sync with iOS12 MDM Controls](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Require iTunes Store password for all purchases**: **Require** users to enter the Apple ID password for each in-app or ITunes purchase. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow purchases without prompting for a password every time.
- **In-app purchases**: **Block** prevents in-app purchases from the store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow store purchases within a running app.
- **Download content from iBook store flagged as 'Erotica'**: **Block** prevents users from downloading media from the iBook store that's tagged as erotica. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to download books with the "Erotica" category.
- **Allow managed apps to write contacts to unmanaged contacts accounts**: **Allow** lets managed apps, such as the Outlook mobile app, to save or sync contact information, including business and corporate contacts, to the built-in iOS/iPadOS Contacts app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent managed apps from saving or syncing contact information to the built-in iOS/iPadOS Contacts app on devices.
  
  To use this setting, set the **Viewing corporate documents in unmanaged apps** setting to **Block**.

- **Ratings region**: Select the ratings region you want to use for allowed downloads. And then select the allowed ratings for **Movies**, **TV Shows**, and **Apps**.

### Settings apply to: Automated device enrollment (supervised)

- **App store**: **Block** prevents access to the app store on supervised devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

  - **Installing apps from App Store**: **Block** doesn't show the app store on the device home screen. Users can continue to use iTunes or the Apple Configurator to install apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the app store on the home screen.
  - **Automatic app downloads**: **Block** prevents automatic downloading of apps bought on other devices and automatic updates to new apps. It doesn't affect updates to existing apps. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow apps bought on other iOS/iPadOS devices to download and update on the device.

- **Explicit iTunes music, podcast, or news content**: **Block** prevents explicit iTunes music, podcast, or news content. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the device to access content rated as adult from the store.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

- **Adding Game Center friends**: **Block** prevents users from adding Game Center friends. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to add friends in Game Center.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

- **Game Center**: **Block** using the Game Center app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Game Center app on devices.
- **Multiplayer gaming**: **Block** prevents multiplayer gaming. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to play multiplayer games on devices.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

- **Access to network drive in Files app**: Using the Server Message Block (SMB) protocol, devices can access files or other resources on a network server. **Disable** prevents accessing files on a network SMB drive. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

## Built-in Apps

### Settings apply to: All enrollment types

- **Siri**: **Block** prevents access to Siri. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Siri voice assistant on devices.
  - **Siri while device is locked**: **Block** prevents access to Siri when devices are locked. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Siri voice assistant on devices when they're locked.

- **Safari fraud warnings**: **Require** fraud warnings to be shown in the web browser on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable this feature.

### Settings apply to: Device enrollment, Automated device enrollment (supervised)


- **Spotlight search to return results from internet**: **Block** stops Spotlight from returning any results from an Internet search. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Spotlight search connect to the Internet to provide search results.

  This setting is duplicated in the UI, and will be fixed in an upcoming release. Currently, this setting applies to supervised devices. In a future release, this setting applies to device enrolled and automated device enrolled devices, and won't require supervision.

- **Safari cookies**: Select how cookies are handled on devices. Your options:
  - Allow
  - Block all cookies
  - Allow cookies from visited web sites
  - Allow cookies from current web site

- **Safari JavaScript**: **Block** prevents Java scripts in the browser from running on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Java scripts.

- **Safari Pop-ups**: **Block** blocks all pop-ups in the Safari web browser. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the pop-up blocker.

### Settings apply to: Automated device enrollment (supervised)

- **Camera**: **Block** prevents access to the camera on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the device's camera.

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

  - **FaceTime**: **Block** prevents access to the FaceTime app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the FaceTime app on devices.

    Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

- **Siri profanity filter**: **Require** prevents Siri from dictating, or speaking profane language. When set to **Not configured** (default), Intune doesn't change or update this setting.

  To use this setting, set the **Siri** setting to **Block**.

  This feature applies to:  
  - iOS 11.0 and newer

- **Siri to query user-generated content from the internet**: **Block** prevents Siri from accessing websites to answer questions. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Siri to access user-generated content from the internet.

  To use this setting, set the **Siri** setting to **Block**.

- **Apple News**: **Block** prevents access to the Apple News app on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Apple News app.
- **iBooks store**: **Block** prevents access to the iBooks store. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to browse and buy books from the iBooks store.
- **Messages app on the device**: **Block** prevents users from using the Messages app for iMessage. If devices support text messaging, users can still send and receive text messages using SMS. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Messages app to send and read messages over the internet.
- **Podcasts**: **Block** prevents users using the Podcasts app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Podcasts app.
- **Music service**: **Block** reverts the Music app to classic mode and disables the Music service. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Apple Music app.
- **iTunes Radio service**: **Block** prevents using the iTunes Radio app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the iTunes Radio app.
- **iTunes store**: **Block** prevents using iTunes on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow iTunes.

  This feature applies to:  
  - iOS 4.0 and newer
  - iPadOS 13.0 and newer

- **Find my iPhone**: **Block** prevents this feature in the Find My app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using this Find My app feature to get the approximate location of the device.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

- **Find my Friends**: **Block** prevents this feature in the Find My app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using this Find My app feature to find family and friends from an Apple device or iCloud.com.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

- **Changes to the Find My Friends app settings**: **Block** prevents changes to the Find My Friends app settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change settings for the Find My Friends app.

- **Spotlight search to return results from internet**: **Block** stops Spotlight from returning any results from an Internet search. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Spotlight search connect to the Internet to provide search results.

  This setting is duplicated in the UI, and will be fixed in an upcoming release. Currently, this setting applies to supervised devices. In a future release, this setting applies to device enrolled and automated device enrolled devices, and won't require supervision.

- **Block removal of system apps from device**: **Block** disables the ability to remove system apps from devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to remove system apps.

- **Safari**: **Block** using the Safari browser on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use the Safari browser.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

- **Safari Autofill**: **Block** disables the autofill feature in Safari on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change autocomplete settings in the web browser.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

## Restricted apps

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Type of restricted apps list**: Create a list of apps that users aren't allowed to install or use. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might allow access to apps you assign, and built-in apps.
  - **Prohibited apps**: List the apps (not managed by Intune) that users aren't allowed to install and run. Users aren't prevented from installing a prohibited app. If a user installs an app from this list, the device is reported in the **Devices with restricted apps** report ([Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Monitor** > **Devices with restricted apps**). 
  - **Approved apps**: List the apps that users are allowed to install. To stay compliant, users must not install other apps. Apps that are managed by Intune are automatically allowed, including the Company Portal app. Users aren't prevented from installing an app that isn't on the approved list. But if they do, it's reported in Intune.

To add apps to these lists, you can:

- **Add** the iTunes App store URL of the app you want. For example, to add the Microsoft Work Folders app, enter `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` or `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`.

  To find the URL of an app, open the iTunes App Store, and search for the app. For example, search for `Microsoft Remote Desktop` or `Microsoft Word`. Select the app, and copy the URL.

  You can also use iTunes to find the app, and then use the **Copy Link** task to get the app URL.

- **Import** a CSV file with details about the app, including the URL. Use the `<app url>, <app name>, <app publisher>` format. Or, **Export** an existing list that includes the restricted apps list in the same format.

> [!IMPORTANT]
> Device profiles that use the restricted app settings must be assigned to groups of users.

## Shared iPad

This feature applies to:

- iPadOS 13.4 and newer
- Shared iPad

### Settings apply to: Automated device enrollment (supervised)

- **Block Shared iPad temporary sessions​**: Temporary sessions allow users to sign in as Guest, and users aren't required to enter a Managed Apple ID or password.

  When set to **Yes**:

  - Shared iPad users can't use temporary sessions.
  - Users must sign in to the device with their Managed Apple ID and password.
  - The Guest account option isn't shown on the lock screen on the devices.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS allows a Shared iPad user to sign in to the device with the Guest account. When the user signs out, none of the user’s data is saved or synced to iCloud.

## Show or hide apps

This feature applies to:

- iOS 9.3 and newer
- iPadOS 13.0 and newer

### Settings apply to: Automated device enrollment (supervised)

- **Type of apps list**: Create a list of apps to show or hide. You can show or hide built-in apps and line-of-business apps. Apple's web site has a list of [built-in Apple apps](https://support.apple.com/HT208094). Your options:

  - **Hidden apps**: Enter a list of apps that are hidden from users. Users can't view, or open these apps.
  
    Apple prevents hiding some native apps. For example, you can't hide the **Settings** app on the device. [Delete built-in Apple apps](https://support.apple.com/HT208094) lists the apps that can be hidden.
  
  - **Visible apps**: Enter a list of apps that users can view and launch. No other apps can be viewed or launched.

- **App URL**: Enter the store app URL of the app you want to show or hide. For example:

  - To add the Microsoft Work Folders app, enter `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` or `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`. 

  - To add the Microsoft Word app, enter `https://itunes.apple.com/de/app/microsoft-word/id586447913` or `https://apps.apple.com/de/app/microsoft-word/id586447913`.

  To find the URL of an app, open the iTunes App Store, and search for the app. For example, search for `Microsoft Remote Desktop` or `Microsoft Word`. Select the app, and copy the URL.

  You can also use iTunes to find the app, and then use the **Copy Link** task to get the app URL.

- **App Bundle ID**: Enter the app [bundle ID](bundle-ids-built-in-ios-apps.md) of the app you want. You can show or hide built-in apps and line-of-business apps. Apple's web site has a list of [built-in Apple apps](https://support.apple.com/HT208094).
- **App name**: Enter the app name of the app you want. You can show or hide built-in apps and line-of-business apps. Apple's web site has a list of [built-in Apple apps](https://support.apple.com/HT208094).
- **Publisher**: Enter the publisher of the app you want.

To add apps, you can:

- **Add**: Select to create your list of apps.
- **Import** a CSV file with details about the app, including the URL. Use the `<app url>, <app name>, <app publisher>` format. Or, **Export** to create a list of the restricted apps you added, in the same format.

## Wireless

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Data roaming**: **Block** prevents data roaming over the cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow data roaming when the device is on a cellular network.

  > [!IMPORTANT]
  > This setting is treated as a remote device action. So, this setting isn't shown in the management profile on devices. Every time the data roaming status changes on the device, **Data roaming** is blocked by the Intune service. In Intune, if the reporting status shows a success, then know that it's working, even though the setting isn't shown in the management profile on the device.

- **Global background fetch while roaming**: **Block** prevents using the global background fetch feature when roaming over the cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow devices to fetch data, such as email, when it's roaming on a cellular network.
- **Voice dialing**: **Block** prevents using the voice dialing feature on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow voice dialing on devices.
- **Voice roaming**: **Block** prevents voice roaming over the cellular network. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow voice roaming when devices are on a cellular network.
- **Personal Hotspot**: **Block** turns off the personal hotspot on devices with every device sync. This setting might not be compatible with some carriers. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might keep the personal hotspot configuration as the default set by users.

  > [!IMPORTANT]
  > This setting is treated as a remote device action. So, this setting isn't shown in the management profile on devices. Every time the personal hotspot status changes on the device, **Personal Hotspot** is blocked by the Intune service. In Intune, if the reporting status shows a success, then know that it's working, even though the setting isn't shown in the management profile on the device.

- **Cellular usage rules (managed apps only)**: **Allow** defines the data types that managed apps can use when on cellular networks. When set to **Not configured** (default), Intune doesn't change or update this setting. Your options:
  - **Block use of cellular data**: Block using cellular data for **All managed apps** or **Choose specific apps**.
  - **Block use of cellular data when roaming**: Block using cellular data when roaming for **All managed apps** or **Choose specific apps**.

### Settings apply to: Automated device enrollment (supervised)

- **Changes to app cellular data usage settings**: **Block** prevents changes to the app cellular data usage settings. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to control which apps are allowed to use cellular data.
- **Changes to cellular plan settings**: **Block** prevents changing any settings in the cellular plan. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to make changes.

  This feature applies to:  
  - iOS 11.0 and newer
  - iPadOS 13.0 and newer

- **User modification of Personal Hotspot**: **Block** prevents changing the personal hotspot setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to enable or disable their personal hotspot.

  If you block this setting and block the **Personal Hotspot** setting, the personal hotspot is turned off.

  This feature applies to:  
  - iOS 12.2 and newer
  - iPadOS 13.0 and newer

- **Join Wi-Fi networks only using configuration profiles**: **Require** forces devices to use only Wi-Fi networks set up through Intune configuration profiles. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow devices to use other Wi-Fi networks.

  When set to **Require**, be sure the device has a Wi-Fi profile. If you don't assign a Wi-Fi profile, this setting could prevent devices from connecting to the internet. In other words, if this device restrictions profile is assigned before a Wi-Fi profile, the device might be blocked from connecting to the internet.
  
  If it can't connect, then unenroll the device, and re-enroll with a Wi-Fi profile. Then, set this setting to **Require** in a device restrictions profile, and assign the profile to the device.

- **Wi-Fi always turned on**: **Require** keeps Wi-Fi on in the Settings app. It can't be turned off in Settings or in the Control Center, even when the device is in airplane mode. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to turn on or turn off Wi-Fi.

  Configuring this setting doesn't prevent users from selecting a Wi-Fi network.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

## Connected Devices

### Settings apply to: All enrollment types

- **Wrist detection for paired Apple watch**: **Require** forces a paired Apple watch to use wrist detection. When required, the Apple Watch won't display notifications when it's not being worn. When set to **Not configured** (default), Intune doesn't change or update this setting.

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Require AirPlay outgoing requests pairing password**: **Require** a pairing password when using AirPlay to stream content to other Apple devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to stream content using AirPlay without entering a password.

### Settings apply to: Automated device enrollment (supervised)

- **AirDrop**: **Block** prevents using AirDrop on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the AirDrop feature to exchange content with nearby devices.
- **Apple Watch pairing**: **Block** prevents pairing with an Apple Watch. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow devices to pair with an Apple Watch.
- **Bluetooth modification**: **Block** stops users from changing Bluetooth settings on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change these settings.
- **Host pairing to control the devices an iOS/iPadOS device can pair with**: **Block** prevents host pairing. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow host pairing to let the administrator control which devices an iOS/iPadOS device can pair with.
- **Block AirPrint**: **Block** prevents using the AirPrint feature on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use AirPrint.
  - **Block storage of AirPrint credentials in Keychain**: **Block** prevents using Keychain storage for username and password on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow storing the AirPrint username and password in the Keychain app.
  - **Require a trusted TLS certificate for AirPrint**: **Require** forces devices to use trusted certificates for TLS printing communication. When set to **Not configured** (default), Intune doesn't change or update this setting.
  - **Block iBeacon discovery of AirPrint printers**: **Block** prevents malicious AirPrint Bluetooth beacons from phishing for network traffic. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow advertising AirPrint printers on devices.
- **Block setting up new nearby devices**: **Block** disables the prompt to set up new devices that are nearby. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow prompts for users to connect to other nearby Apple devices.

  This feature applies to:  
  - iOS 11.0 and newer
  - iPadOS 13.0 and newer

- **Access to files on USB drive**: Devices can connect and open files on a USB drive. **Disable** prevents device access to the USB drive in the Files app when a USB is connected to the device. Disabling this feature also blocks users from transferring files onto a USB drive connected to an iPad. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to a USB drive in the Files app.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

## Keyboard and Dictionary

### Settings apply to: Automated device enrollment (supervised)

- **Word definition lookup**: **Block** prevents highlighting a word, and then looking up its definition. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the definition lookup feature.
- **Predictive keyboards**: **Block** prevents using predictive keyboards to suggest words users might want. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.
- **Auto-correction**: **Block** prevents using autocorrection. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow devices to automatically correct misspelled words.
- **Keyboard spell-check**: **Block** prevents spell checker. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using spellchecker.
- **Keyboard shortcuts**: **Block** stops users from using keyboard shortcuts. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using keyboard shortcuts on devices.
- **Dictation**: **Block** stops users from using voice input to enter text. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use dictation input.
- **QuickPath**: **Block** prevents users from using QuickPath. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use QuickPath, which allows a continuous input on the device's keyboard. Users can type by swiping across the keys to create words.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

## Cloud and Storage

### Settings apply to: All enrollment types

- **Encrypted backup**: **Require** so device backups must be encrypted. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Managed apps sync to cloud**: **Block** prevents Intune-managed apps to sync data to the user's iCloud account. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this data sync to iCloud.
- **Block Enterprise Book Backup**: **Block** prevents backing up enterprise books. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to back up these books.
- **Block enterprise book metadata sync (notes and highlights)**: **Block** prevents syncing notes and highlights in enterprise books. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the syncing.

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Photo stream syncing to iCloud**: **Block** prevents photo stream syncing to iCloud. Blocking this feature may cause data loss. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might let users enable **My Photo Stream** on their device to sync to iCloud, and have photos available on all the user's devices.
- **iCloud Photo Library**: **Block** disables using iCloud photo library to store photos and videos in the cloud. Any photos not fully downloaded from iCloud Photo Library to devices are removed from the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the iCloud photo library.
- **Shared photo stream**: **Block** disables **iCloud Photo Sharing** on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow shared photo streaming.
- **Handoff**: **Block** prevents users from starting work on an iOS/iPadOS device, and then continuing the work on another iOS/iPadOS or macOS device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this handoff.

### Settings apply to: Automated device enrollment (supervised)

- **Backup to iCloud**: **Block** stops users from backing up devices to iCloud. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to back up devices to iCloud.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

- **Block iCloud Document sync**: **Block** prevents iCloud from syncing documents and data. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow document and key-value synchronization to your iCloud storage space.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

- **Block iCloud Keychain sync**: **Block** disables syncing credentials stored in the Keychain to iCloud. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to sync these credentials.

  Starting with iOS/iPadOS 13.0, this setting requires supervised devices.

## Autonomous single app mode (ASAM)

Use these settings to configure iOS/iPadOS devices to run specific apps in autonomous single app mode (ASAM). When ASAM is configured, and users start one of the configured apps, then the device is locked to that app. App/task switching is disabled until users exit the allowed app.

For the ASAM configuration to apply, users must manually open the specific app. This task also applies to the Company Portal app.

- For example, in a school or university environment, add an app that lets users take a test on the device. Or, lock the device into the Company Portal app until the user authenticates. When the apps actions are completed by users, or you remove this policy, the device returns to its normal state.

- Not all apps support autonomous single app mode. To put an app in ASAM, a bundle ID or a key value pair delivered by an app config policy are typically required. For more information, see the [`autonomousSingleAppModePermittedAppIDs` restriction](https://developer.apple.com/documentation/devicemanagement/restrictions) in Apple's MDM documentation. For more information on the specific settings required for the app you're configuring, see the vendor documentation.

  For example, to configure Zoom Rooms in autonomous single app mode, Zoom says to use the `us.zoom.zpcontroller` bundle ID. In this instance, you also make a change in the Zoom web portal. For more information, see the [Zoom help center](https://support.zoom.us/hc/articles/360021322632-Autonomous-Single-App-Mode-for-Zoom-Rooms-with-a-Third-Party-MDM).

- On iOS/iPadOS devices, the Company Portal app supports ASAM. When the Company Portal app is in ASAM, users must manually open the Company Portal app. Then the device is locked in the Company Portal app until the user authenticates. When users sign in to the Company Portal app, they can use other apps and the Home screen button on the device. When they sign out of the Company Portal app, the device returns to single app mode, and locks on the Company Portal app.

  To turn the Company Portal app into a 'sign in/sign out' app (enable ASAM), enter the Company Portal app name, such as `Microsoft Intune Company Portal`, and the bundle ID (`com.microsoft.CompanyPortal`) in these settings. After this profile is assigned, you must open the Company Portal app to lock the app so users can sign in and sign out of it. For the ASAM configuration to apply, users must manually open the Company Portal app.
  
  When the device configuration profile is removed, and the user signs out, the device isn't locked in the Company Portal app.

### Settings apply to: Automated device enrollment (supervised)

- **App name**: Enter the name of the app you want.
- **App Bundle ID**: Enter the [bundle ID](bundle-ids-built-in-ios-apps.md) of the app you want.
- **Add**: Select to create your list of apps.

You can also **Import** a CSV file with the list of app names and their bundle IDs. Or, **Export** an existing list that includes the apps.

## Kiosk

[Single App Mode](https://support.apple.com/guide/mdm/mdm80a981/web) is referred to as Kiosk mode in Intune.

### Settings apply to: Automated device enrollment (supervised)

- **App to run in kiosk mode**: Select the type of apps you want to run in kiosk mode. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might not apply kiosk settings. The device doesn't run in kiosk-mode.
  - **Store App**: Enter the URL to an app in the iTunes App store.
  - **Managed App**: Select an app you previously added to Intune.
  - **Built-In App**: Enter the [bundle ID](bundle-ids-built-in-ios-apps.md) of the built-in app.

- **Assistive touch**: **Require** the Assistive Touch accessibility setting be on devices. This feature helps users with on-screen gestures that might be difficult for them. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not run or enable this feature in kiosk mode.
- **Invert colors**: **Require** the Invert Colors accessibility setting so users with visual impairments can change the display screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not run or enable this feature in kiosk mode.
- **Mono audio**: **Require** the Mono audio accessibility setting be on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not run or enable this feature in kiosk mode.
- **Voice control**: **Require** enables voice control on devices, and allows users to fully control the OS using Siri commands. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable voice control.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer
  
  > [!TIP]
  > If you have LOB apps available for your organization, and they're not **Voice Control** ready on day 0 when iOS 13.0 releases, then we recommend you leave this setting as **Not configured**.

- **VoiceOver**: **Require** the VoiceOver accessibility setting to read text on the screen out loud. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not run or enable this feature in kiosk mode.
- **Zoom**: **Require** the Zoom setting so users can touch to zoom in on the screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not run or enable this feature in kiosk mode.
- **Auto lock**: **Block** prevents automatic locking of devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.
- **Ringer switch**: **Block** disables the ringer (mute) switch on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.
- **Screen rotation**: **Block** prevents changing the screen orientation when users rotate the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.
- **Screen sleep button**: **Block** disables the screen sleep wake button on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature.
- **Touch**: **Block** disables the touchscreen on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use the touchscreen.
- **Volume buttons**: **Block** prevents using the volume buttons on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the volume buttons.
- **Assistive touch control**: **Allow** lets users use the assistive touch function. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable this feature.
- **Invert colors control**: **Allow** inverts color changes to let users adjust the invert colors function. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable this feature.
- **Speak on selected text**: **Allow** the Speak Selection accessibility settings be on devices. This feature reads text out loud that users select. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable this feature.
- **Voice control modification**: **Allow** users to change the state of voice control on their devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might block users from changing the state of voice control on their devices.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

- **VoiceOver control**: **Allow** voiceover changes to let users update the VoiceOver function, such as how fast on-screen text is read out loud. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent voiceover changes.
- **Zoom control**: **Allow** zoom changes by users. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent zoom changes.

> [!NOTE]
> Before you can configure an iOS/iPadOS device for kiosk mode, you must use the Apple Configurator tool or the Apple Device Enrollment Program to put devices into supervised mode. See Apple's guide on using the Apple Configurator tool.
> If the iOS/iPadOS app you enter is installed after you assign the profile, then the device doesn't enter kiosk mode until the device is restarted.

## Domains

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Unmarked email domains** > **Email Domain URL**: Add one or more URLs to the list. When users receive an email from a domain other than the domains you enter, the email is marked as untrusted in the iOS/iPadOS Mail app.

- **Managed web domains** > **Web Domain URL**; Add one or more URLs to the list. When documents are downloaded from the domains you enter, they're considered managed. This setting applies only to documents downloaded using the Safari browser.

### Settings apply to: Automated device enrollment (supervised)

- **Safari password autofill domains** > **Domain URL**: Add one or more URLs to the list. Users can only save web passwords from URLs in this list. This setting applies only to the Safari browser, and devices in supervised mode. If you don't enter any URLs, then passwords can be saved from all web sites.

  This feature applies to:  
  - iOS 9.3 and newer
  - iPadOS 13.0 and newer

## Settings that require supervised mode

iOS/iPadOS supervised mode can only be enabled during initial device setup through Apple's Device Enrollment Program, or by using Apple Configurator. Once supervised mode is enabled, Intune can configure a device with the following functionality:

- Kiosk Mode (Single App Mode): Referred to as "app lock" in the [Apple developer documentation](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf).
- Disable Activation Lock 
- Autonomous Single App Mode 
- Web Content Filter 
- Set background and lock screen 
- Silent App Push 
- Always-On VPN 
- Allow managed app installation exclusively 
- iBookstore 
- iMessages 
- Game Center 
- AirDrop 
- AirPlay 
- Host pairing 
- Cloud Sync 
- Spotlight search 
- Handoff 
- Erase device 
- Restrictions UI 
- Installation of configuration profiles by UI 
- News 
- Keyboard shortcuts 
- Passcode modifications 
- Device name changes 
- Automatic app downloads 
- Apple Music 
- Mail Drop 
- Pair with Apple Watch 

> [!NOTE]
> Apple confirmed that certain settings move to supervised-only in 2019. We recommend taking this into consideration when using these settings, instead of waiting for Apple to migrate them to supervised-only:
>
> - App installation by end users
> - App removal
> - FaceTime
> - Safari
> - iTunes
> - Explicit content
> - iCloud documents and data
> - Multiplayer gaming
> - Add Game Center friends
> - Siri

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also restrict device features and settings on [macOS](device-restrictions-macos.md) devices.
