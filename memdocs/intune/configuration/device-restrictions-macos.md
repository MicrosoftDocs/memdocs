---
# required metadata

title: macOS device settings in Microsoft Intune
titleSuffix:
description: Add, configure, or create settings on macOS devices to restrict features in Microsoft Intune. Set password requirements, control the locked screen, use built-in apps, add restricted or approved apps, handle bluetooth devices, connect to the cloud for backup and storage, enable kiosk mode, add domains, and control how users interact with the Safari web browser.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/20/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: beflamm, jayeren
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# macOS device settings to allow or restrict features using Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article describes the settings you can control and restrict on macOS devices. As part of your mobile device management (MDM) solution, use these settings to allow or disable features, set password rules, allow or restrict specific apps, and more.

This feature applies to:

- macOS

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

> [!NOTE]
> The user interface may not match the enrollment types in this article. The information in this article is correct. The user interface is being updated in an upcoming release.

## Before you begin

Create a [macOS device restrictions configuration profile](device-restrictions-configure.md).

> [!NOTE]
> These settings apply to different enrollment types. For more information on the different enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## App Store, doc viewing, gaming  

### Settings apply to: Automated device enrollment (supervised)

- **Block adding Game Center friends**: **Yes** prevents users from adding friends to Game Center. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to add friends to Game Center.  

  This feature applies to:  
  - macOS 10.13 and newer  

- **Block Game Center**: **Yes** disables Game Center, and the Game Center icon is removed from the home screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might make Game Center available to users.   

  This feature applies to:
  - macOS 10.13 and newer  

- **Block multiplayer gaming in the Game Center**: **Yes** prevents multiplayer gaming when using Game Center. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to play multiplayer games. 

  This feature applies to:  
  - macOS 10.13 and newer  

## Built-in Apps

### Settings apply to: All enrollment types

- **Block Safari AutoFill**: **Yes** disables the autofill feature in Safari on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change autocomplete settings in the web browser.
- **Block use of camera**: **Yes** prevents access to the camera on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow access to the device camera.

  Intune only manages access to the device camera. It doesn't have access to pictures or videos.
  
- **Block Apple Music**: **Yes** reverts the Music app to classic mode, and disables the Music service. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the Apple Music app.
- **Block spotlight suggestions**: **Yes** stops Spotlight from returning any results from an Internet search. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Spotlight search to connect to the Internet, and get search results.
- **Block file transfer using Finder or iTunes**: **Yes** disables application file sharing services. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow application file sharing services.

  This feature applies to:  
  - macOS 10.13 and newer

## Cloud and storage

### Settings apply to: All enrollment types

- **Block iCloud Keychain sync**: **Yes** disables syncing credentials stored in the Keychain to iCloud. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to sync these credentials.
- **Block iCloud Document and Data Sync**: **Yes** prevents iCloud from syncing documents and data. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow document and key-value synchronization to your iCloud storage space.
- **Block iCloud Mail Backup**: **Yes** prevents iCloud from syncing to the macOS Mail app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Mail synchronization to iCloud.
- **Block iCloud Contact Backup**: **Yes** prevents iCloud from syncing the device contacts. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow contact sync using iCloud.
- **Block iCloud Calendar Backup**: **Yes** prevents iCloud from syncing to the macOS Calendar app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Calendar synchronization to iCloud.
- **Block iCloud Reminder Backup**: **Yes** prevents iCloud from syncing to the macOS Reminders app. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Reminders synchronization to iCloud.
- **Block iCloud Bookmark Backup**: **Yes** prevents iCloud from syncing the device Bookmarks. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Bookmark synchronization to iCloud.
- **Block iCloud Notes Backup**: **Yes** prevents iCloud from syncing the device Notes. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow Notes synchronization to iCloud.
- **Block iCloud Photos backup**: **Yes** disables iCloud Photo Library, and prevents iCloud from syncing the device photos. Any photos not fully downloaded from iCloud Photo Library are removed from local storage on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow syncing photos between the device and the iCloud Photo Library.
- **Block Handoff**: This feature allows users to start work on a macOS device, and then continue the work they started on another iOS/iPadOS or macOS device. **Yes** prevents the Handoff feature on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature on devices.

  This feature applies to:  
  - macOS 10.15 and newer

### Settings apply to: User approved device enrollment, Automated device enrollment (supervised)

- **Block iCloud Private Relay**: **Yes** disables the iCloud Private Relay. When disabled, Apple doesn't encrypt internet traffic leaving the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow this feature, which prevents networks and servers from monitoring a user's activity across the internet.

  This feature applies to:  
  - macOS 12 and newer

  [iCloud Private Relay](https://support.apple.com/HT212614) (opens Apple's web site)

## Connected devices

### Settings apply to: All enrollment types

- **Block AirDrop**: **Yes** prevents using AirDrop on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the AirDrop feature to exchange content with nearby devices.
- **Block Apple Watch auto unlock**: **Yes** prevents users from unlocking their macOS device with their Apple Watch. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock their macOS device with their Apple Watch.

## Domains

### Settings apply to: All enrollment types

- **Unmarked Email Domains**: Enter one or more **Email domain URLs** to the list. When users send or receive an email from a domain other than the domains you added, the email is marked as untrusted in the macOS Mail app.

## General

### Settings apply to: All enrollment types

- **Block Lookup**: **Yes** prevents user from highlighting a word, and then looking up its definition on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the definition lookup feature.
- **Block dictation**: **Yes** stops users from using voice input to enter text. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use dictation input.
- **Block content caching**: **Yes** prevents content caching. Content caching stores app data, web browser data, downloads, and more locally on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable content caching.

  For more information on content caching on macOS, see [Manage content caching on Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (opens another website).

  This feature applies to:  
  - macOS 10.13 and newer

- **Block screenshots and screen recording**: **Yes** prevents users from saving screenshots of the display. It also prevents the Classroom app from observing remote screens. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to capture screenshots, and allows the Classroom app to view remote screens.

### Settings apply to: User approved device enrollment, Automated device enrollment (supervised)

- **Defer software updates**: This setting lets you defer the visibility of software updates on devices for up to 90 days. For example, if Apple releases a macOS update on a specific date, it naturally shows on devices around the release date. This setting can hide the update so that users don't see it as soon as it's available.

  This setting doesn't control when updates are installed and doesn't impact scheduled updates. Seed build updates are allowed without delay.

  To use this setting, select the software updates you want to delay. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might show newly released software updates to users as soon as they're released.
  - **Major OS software updates**: Major OS software updates, such as macOS 12, are deferred for 30 days by default, unless otherwise specified in the **Delay visibility of major OS software updates** field. Requires macOS 11.3 and newer.
  - **Minor OS software updates**: Minor OS software updates, such as macOS 12.x, are deferred for 30 days by default, unless otherwise specified in the **Delay visibility of minor OS software updates** field. Requires macOS 11.3 and newer.  
  - **Non-OS software updates**: Non-OS software updates, such as Safari updates, are deferred for 30 days by default, unless otherwise specified in the **Delay visibility of non OS software updates** field. Requires macOS 11.0 and later.
  
  Then enter how long you want to delay each type of update, from 1-90 days. For example, if a macOS update is available on January 1, and **Delay visibility** is set to 5 days, then the update isn't shown as an available update. On the sixth day following the release, that update becomes available, and users are notified to update to the earliest version available when the delay was triggered. Your options:

  - **Delay default visibility of software updates**: Enter the number of days to delay all software updates, from 1-90. If you don't enter anything, updates will be deferred for 30 days, by default. Intune will override this value if you choose to delay major OS, minor OS, or non-OS software updates individually.  
  - **Delay visibility of major OS software updates**: Enter the number of days to delay all major OS software updates, from 1-90. If you don't enter anything, updates will be deferred for 30 days, by default. This value overrides the value in **Delay default visibility of software updates**.  

     This feature applies to:  
    - macOS 11.3 and newer

  - **Delay visibility of minor OS software updates**: Enter the number of days to delay all minor OS software updates, from 1-90. If you don't enter anything, updates will be deferred for 30 days, by default. This value overrides the value in **Delay default visibility of software updates**.

     This feature applies to:  
    - macOS 11.3 and newer

  - **Delay visibility of non-OS software updates**: Enter the number of days to delay all non-OS software updates, from 1-90. If you don't enter anything, updates will be deferred for 30 days, by default. This value overrides the value in **Delay default visibility of software updates**.

     This feature applies to:  
    - macOS 11.0 and newer
  
  - **Allow activation lock**: **Yes**, enables Activation Lock on supervised macOS devices. Activation Lock makes it harder for a lost or stolen device to be reactivated. When set to **Not configured** (default), Intune doesn't change or update this setting.

     This feature applies to:  
    - macOS 10.15 or later  

### Settings apply to: Automated device enrollment  

- **Disable AirPlay, view screen by Classroom app, and screen sharing**: **Yes** blocks AirPlay, and prevents screen sharing to other devices. It also prevents teachers from using the Classroom app to see their students' screens. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow teachers to see their students' screens.

  To use this setting, set the **Block screenshots and screen recording** setting to **Not configured** (screenshots are allowed).

- **Allow Classroom app to perform AirPlay and view screen without prompting**: **Yes** lets teachers see their students' screens without requiring students to agree. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might require students to agree before teachers can see the screens.

  To use this setting, set the **Block screenshots and screen recording** setting to **Not configured** (screenshots are allowed).

- **Require teacher permission to leave Classroom app unmanaged classes**: **Yes** forces students enrolled in an unmanaged Classroom course to get teacher approval to leave the course. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow students to leave the course whenever the student chooses.

- **Allow Classroom to lock the device without prompting**: **Yes** lets teachers lock a student's device or app without the student's approval. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might require students agree before teachers can lock the device or app.

- **Students can automatically join Classroom class without prompting**: **Yes** lets students join a class without prompting the teacher. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might require teacher approval to join a class.  

- **Block modification of wallpaper**:
**Yes** prevents users from changing the device wallpaper. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to change the wallpaper.  

  This feature applies to:  
  - macOS 10.13 and newer  

- **Block users from erasing all content and settings on device**: **Yes** disables the reset option on supervised devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to erase all content and settings on their device.  

  This feature applies to:  
  - macOS 12 and newer  

## Password

These settings use the [Passcode payload](https://developer.apple.com/documentation/devicemanagement/passcode) (opens Apple's web site).

> [!IMPORTANT]
>
> - On macOS devices running 10.14.2 and later (except all versions of macOS 10.15 Catalina), users are prompted to change the device password when the device updates to a new major OS version. This password update happens once. After users update the password, any other password policies are enforced. If a passcode is required in at least one policy, then this behavior only occurs for the local machine user.
>
> - Any time the password policy is updated, all users running these macOS versions must change the password, even if the current password is compliant with the new requirements. For example, when your macOS device turns on after upgrading to a new major OS version such as Big Sur (macOS 11) or Monterey (macOS 12), users need to change the device password before they can sign in.

### Settings apply to: All enrollment types

- **Require password**: **Yes** requires users to enter a password to access devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require a password. It also doesn't force any restrictions, such as blocking simple passwords or setting a minimum length.
  - **Required password type**: Enter the required password complexity level your organization requires. When left blank, Intune doesn't change or update this setting. Your options:
    - **Not configured**: Uses the device default.
    - **Alphanumeric**: Includes uppercase letters, lowercase letters, and numeric characters.
    - **Numeric**: Password must only be numbers, such as 123456789.

    This feature applies to:  
    - macOS 10.10.3 and newer

  - **Number of non-alphanumeric characters in password**: Enter the number of complex characters required in the password, from 0-4. A complex character is a symbol, such as `?`. When left blank or set to **Not configured**, Intune doesn't change or update this setting.
  - **Minimum password length**: Enter the minimum length the password must have, from 4-16 characters. When left blank, Intune doesn't change or update this setting.
  - **Block simple passwords**: **Yes** prevents using simple passwords, such as `0000` or `1234`. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting. By default, the OS might allow simple passwords.
  - **Maximum minutes of inactivity until screen locks**: Enter the length of time devices must be idle before the screen is automatically locked. For example, enter `5` to lock devices after 5 minutes of being idle. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.
  - **Maximum minutes after screen lock before password is required**: Enter the length of time devices must be inactive before a password is required to unlock it. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.
  - **Password expiration (days)**: Enter the number of days until the device password must be changed, from 1-65535. For example, enter `90` to expire the password after 90 days. When the password expires, users are prompted to create a new password. When the value is blank or set to **Not configured**, Intune doesn't change or update this setting.
  - **Prevent reuse of previous passwords**: Restrict users from creating previously used passwords. Enter the number of previously used passwords that can't be used, from 1-24. For example, enter 5 so users can't set a new password to their current password or any of their previous four passwords. When the value is blank, Intune doesn't change or update this setting.
  - **Maximum allowed sign-in attempts**: Enter the maximum number of times that users can consecutively try to sign in before the device locks users out, from 2-11. When this number is exceeded, the device is locked. We recommend not setting this value to a low number, such as `2` or `3`. It's common for users to enter the wrong password. We recommend setting to a higher value.

    For example, enter `5` so users can enter the wrong password up to five times. After the fifth attempt, the device is locked. If you leave this value blank, or don't change it, then `11` is used by default.

    After six failed attempts, macOS automatically forces a time delay before a passcode can be entered again. The delay increases with each attempt. Set the **Lockout duration** to add a delay before the next passcode can be entered.

    - **Lockout duration**: Enter the number of minutes a lockout lasts, from 0-10000. During a device lockout, the sign-in screen is inactive, and users can't sign in. When the lockout ends, user can try to sign in again.

      If you leave this value blank, or don't change it, then `30` minutes is used by default.

      This setting applies to:

      - macOS 10.10 and newer

- **Block user from modifying passcode**: **Yes** stops the passcode from being changed, added, or removed. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passcodes to be added, changed, or removed.

- **Block Touch ID to unlock device**: **Yes** prevents using fingerprints to unlock devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using a fingerprint.

- **Timeout (hours of inactivity)**: Enter a value of inactive hours that users must enter their password, instead of TouchID.

  The default inactivity period is 48 hours. After 48 hours of inactivity, the device prompts for the password, instead of Touch ID.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might set the timeout to 48 hours (172,800 seconds).

  This feature applies to:  
  - macOS 12 and newer

- **Block password AutoFill**: **Yes** prevents using the AutoFill Passwords feature on macOS. Choosing **Yes** also has the following impact:

  - Users aren't prompted to use a saved password in Safari or in any apps.
  - Automatic Strong Passwords are disabled, and strong passwords aren't suggested to users.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these features.

- **Block password proximity requests**: **Yes** prevents devices from requesting passwords from nearby devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these password requests.

- **Block password sharing**: **Yes** prevents sharing passwords between devices using AirDrop. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passwords to be shared.

## Privacy preferences

On macOS devices, apps and processes often prompt users to allow or deny access to device features, such as the camera, microphone, calendar, Documents folder, and more. These settings allow administrators to pre-approve or pre-deny access to these device features. When you configure these settings, you manage data access consent on behalf of your users. Your settings override their previous decisions.

The goal of these settings is to reduce the number of prompts by apps and processes.

This feature applies to:

- macOS 10.14 and newer
- Some settings apply to macOS 10.15 and newer.
- These settings only apply on devices that have the privacy preferences profile installed before being upgraded.

### Settings apply to: User approved device enrollment, Automated device enrollment

- **Apps and processes**: **Add** apps or processes to configure access. Also enter:
  - **Name**: Enter a name for your app or process. For example, enter `Microsoft Remote Desktop` or `Microsoft 365`.
  
  - **Identifier type**: Your options:
    - **Bundle ID**: Select this option for apps.
    - **Path**: Select this option for non-bundled binaries, which is a process or executable.

    Helper tools embedded within an application bundle automatically inherit the permissions of their enclosing application bundle.

  - **Identifier**: Enter the app bundle ID, or the installation file path of the process or executable. For example, enter `com.contoso.appname`.

    To get the app bundle ID, open the Terminal app, and run the `codesign` command. This command identifies the code signature. So you can get the bundle ID and the code signature simultaneously.

  - **Code requirement**: Enter the code signature for the application or process.

    A code signature is created when an app or binary is signed by a developer certificate. To find the designation, run the `codesign` command manually in the Terminal app: `codesign --display -r - /path/to/app/binary`. The code signature is everything that appears after `=>`.

  - **Enable static code validation**: Choose **Yes** for the app or process to statically validate the code requirement. When set to **Not configured**, Intune doesn't change or update this setting.

    Enable this setting only if the process invalidates its dynamic code signature. Otherwise, use **Not configured**.  

  - **Block Camera**: **Yes** prevents the app from accessing the system camera. You can't allow access to the camera. When set to **Not configured**, Intune doesn't change or update this setting.

  - **Block Microphone**: **Yes** prevents the app from accessing the system microphone. You can't allow access to the microphone. When set to **Not configured**, Intune doesn't change or update this setting.

  - **Block screen recording**: **Yes** blocks the app from capturing the contents of the system display. You can't allow access to screen recording and screen capture. When set to **Not configured**, Intune doesn't change or update this setting.

    Requires macOS 10.15 and newer.

  - **Block input monitoring**: **Yes** blocks the app from using CoreGraphics and HID APIs to listen to CGEvents and HID events from all processes. **Yes** also denies apps and processes from listening to and collecting data from input devices, such as a mouse, keyboard, or trackpad. You can't allow access to the CoreGraphics and HID APIs.

    When set to **Not configured**, Intune doesn't change or update this setting.

    Requires macOS 10.15 and newer.

  - **Speech recognition**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access the system speech recognition, and allows sending speech data to Apple.
    - **Block**: Prevents the app from accessing the system speech recognition, and prevents sending speech data to Apple.

    Requires macOS 10.15 and newer.

  - **Accessibility**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access to the system Accessibility app. This app includes closed captions, hover text, and voice control.
    - **Block**: Prevents the app from accessing the system Accessibility app.

  - **Contacts**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access contact information managed by the system Contacts app.  
    - **Block**: Prevents the app from accessing this contact information.

  - **Calendar**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access calendar information managed by the system Calendar app.
    - **Block**: Prevents the app from accessing this calendar information.

  - **Reminders**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access reminder information managed by the system Reminders app.
    - **Block**: Prevents the app from accessing this reminder information.

  - **Photos**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access the pictures managed by the system Photos app in `~/Pictures/.photoslibrary`.
    - **Block**: Prevents the app from accessing these pictures.

  - **Media library**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access Apple Music, music and video activity, and the media library.  
    - **Block**: Prevents the app from accessing this media.

    Requires macOS 10.15 and newer.

  - **File provider presence**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access the File Provider app, and know when users are using files managed by the File Provider. A File Provider app allows other File Provider apps to access the documents and directories stored and managed by the containing app.
    - **Block**: Prevents the app from accessing the File Provider app.

    Requires macOS 10.15 and newer.

  - **Full disk access**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access all protected files, including system administration files. Apply this setting with caution.
    - **Block**: Prevents the app from accessing these protected files.

  - **System admin files**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access some files used in system administration.
    - **Block**: Prevents the app from accessing these files.

  - **Desktop folder**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access files in the user's Desktop folder.
    - **Block**: Prevents the app from accessing these files.

    Requires macOS 10.15 and newer.

  - **Documents folder**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access files in the user's Documents folder.
    - **Block**: Prevents the app from accessing these files.

    Requires macOS 10.15 and newer.

  - **Downloads folder**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access files in the user's Downloads folder.
    - **Block**: Prevents the app from accessing these files.

    Requires macOS 10.15 and newer.

  - **Network volumes**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access files on network volumes.
    - **Block**: Prevents the app from accessing these files.

    Requires macOS 10.15 and newer.

  - **Removable volumes**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to access files on removable volumes, such as a hard disk.
    - **Block**: Prevents the app from accessing these files.

    Requires macOS 10.15 and newer.

  - **System events**: Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **Allow**: Allows the app to use CoreGraphics APIs to send CGEvents to the system event stream.
    - **Block**: Prevents the app from using CoreGraphics APIs to send CGEvents to the system event stream.

  - **Apple events**: This setting allows apps to send a restricted Apple event to another app or process. Select **Add** to add a receiving app or process. Enter the following information of the receiving app or process:

    - **Identifier type**: Select **Bundle ID** if the receiving identifier is an application. Select **Path** if the receiving identifier is a process or executable.

    - **Identifier**: Enter the app bundle ID, or the installation path of the process receiving an Apple event.  

    - **Code requirement**: Enter the code signature for the receiving application or process.

      A code signature is created when an app or binary is signed by a developer certificate. To find the designation, run the `codesign` command manually in the Terminal app: `codesign --display -r -/path/to/app/binary`. The code signature is everything that appears after `=>`.

    - **Access**: Allow a macOS Apple Event to be sent to the receiving app or process. Your options:
      - **Not configured**: Intune doesn't change or update this setting.
      - **Allow**: Allows the app or process to send the restricted Apple event to the receiving app or process.
      - **Block**: Prevents the app or process from sending a restricted Apple event to the receiving app or process.

  - **Save** your changes.

## Restricted apps

### Settings apply to: All enrollment types

- **Type of restricted apps list**: Create a list of apps that users aren't allowed to install or use. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, users might have access to apps you assign, and built-in apps.
  - **Approved apps**: List the apps that users are allowed to install. Users must not install other apps. If users install apps that aren't allowed, then it's reported in Intune. Apps that are managed by Intune are automatically allowed, including the Company Portal app. Users aren't prevented from installing an app that isn't on the approved list.
  - **Prohibited apps**: List the apps (not managed by Intune) that users aren't allowed to install and run. Users aren't prevented from installing a prohibited app. If a user installs an app from this list, it's reported in Intune.

- **Apps list**: **Add** apps to your list:
  - **App Bundle ID**: Enter the [bundle ID](bundle-ids-built-in-ios-apps.md) of the app. You can add built-in apps and line-of-business apps. Apple's web site has a list of [built-in Apple apps](https://support.apple.com/HT208094).

    To find the bundle ID of a macOS app, you can open the Terminal app, and use AppleScript (`osascript -e 'id of app "AppName"'`).

    To find the URL of an app, open the iTunes App Store, and search for the app. For example, search for `Microsoft Remote Desktop` or `Microsoft Word`. Select the app, and copy the URL. You can also use iTunes to find the app, and then use the **Copy Link** task to get the app URL.

  - **App name**: Enter a user-friendly name to help you identify the bundle ID. For example, enter `Intune Company Portal app`.
  - **Publisher**: Enter the publisher of the app.

- **Import** a CSV file with details about the app, including the URL. Use the `<app bundle ID>, <app name>, <app publisher>` format. Or, **Export** to create a list of apps you added, in the same format.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also restrict device features and settings on [iOS/iPadOS](device-restrictions-ios.md) devices.
