---
# required metadata

title: macOS device settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add, configure, or create settings on macOS devices to restrict features, including setting password requirements, control the locked screen, use built-in apps, add restricted or approved apps, handle bluetooth devices, connect to the cloud for backup and storage, enable kiosk mode, add domains, and control how users interact with the Safari web browser in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# macOS device settings to allow or restrict features using Intune

This article lists and describes the different settings you can control on macOS devices. As part of your mobile device management (MDM) solution, use these settings to allow or disable features, set password rules, allow or restrict specific apps, and more.

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

> [!NOTE]
> The user interface may not match the enrollment types in this article. The information in this article is correct. The user interface is being updated in an upcoming release.

## Before you begin

[Create a macOS device restrictions configuration profile](device-restrictions-configure.md).

> [!NOTE]
> These settings apply to different enrollment types. For more information on the different enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

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
- **Block iCloud Desktop and Document Sync**: **Yes** prevents iCloud from syncing documents and data. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow document and key-value synchronization to your iCloud storage space.
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

## Connected devices

### Settings apply to: All enrollment types

- **Block AirDrop**: **Yes** prevents using AirDrop on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using the AirDrop feature to exchange content with nearby devices.
- **Block Apple Watch auto unlock**: **Yes** prevents users from unlocking their macOS device with their Apple Watch. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock their macOS device with their Apple Watch.

## Domains

### Settings apply to: All enrollment types

- **Unmarked Email Domains**: Enter one or more **Email domain URL** to the list. When users send or receive an email from a domain other than the domains you added, the email is marked as untrusted in the macOS Mail app.

## General

### Settings apply to: All enrollment types

- **Block Lookup**: **Yes** prevents user from highlighting a word, and then looking up its definition on the device. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the definition lookup feature.
- **Block dictation**: **Yes** stops users from using voice input to enter text. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to use dictation input.
- **Block content caching**: **Yes** prevents content caching. Content caching stores app data, web browser data, downloads, and more locally on devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might enable content caching.

  For more information on content caching on macOS, see [Manage content caching on Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (opens another website).

  This feature applies to:  
  - macOS 10.13 and newer

- **Defer software updates**: **Yes** allows you to delay when software updates are shown on devices, from 0-90 days. This setting doesn't control when updates are or aren't installed. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show updates on devices as Apple releases them. For example, if a macOS update gets released by Apple on a specific date, then that update naturally shows up on devices around the release date. Seed build updates are allowed without delay.  

  - **Delay visibility of software updates**: Enter a value from 0-90 days. When the delay expires, users get a notification to update to the earliest version of the OS available when the delay was triggered.

    For example, if a macOS update is available on **January 1**, and **Delay visibility** is set to **5 days**, then the update isn't shown as an available update. On the **sixth day** following the release, that update is available, and users can install it.

    This feature applies to:  
    - macOS 10.13.4 and newer

- **Block screenshots and screen recording**: Device must be enrolled in Apple's Automated Device Enrollment (DEP). **Yes** prevents users from saving screenshots of the display. It also prevents the Classroom app from observing remote screens. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to capture screenshots, and allows the Classroom app to view remote screens.

  - **Disable AirPlay, view screen by Classroom app, and screen sharing**: **Yes** blocks AirPlay, and prevents screen sharing to other devices. It also prevents teachers from using the Classroom app to see their students' screens. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow teachers to see their students' screens.

    To use this setting, set the **Block screenshots and screen recording** setting to **Not configured** (screenshots are allowed).

  - **Allow Classroom app to perform AirPlay and view screen without prompting**: **Yes** lets teachers see their students' screens without requiring students to agree. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might require students to agree before teachers can see the screens.

    To use this setting, set the **Block screenshots and screen recording** setting to **Not configured** (screenshots are allowed).

- **Require teacher permission to leave Classroom app unmanaged classes**: **Yes** forces students enrolled in an unmanaged Classroom course to get teacher approval to leave the course. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow students to leave the course whenever the student chooses.

- **Allow Classroom to lock the device without prompting**: **Yes** lets teachers lock a student's device or app without the student's approval. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might require students agree before teachers can lock the device or app.

- **Students can automatically join Classroom class without prompting**: **Yes** lets students join a class without prompting the teacher. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might require teacher approval to join a class.

## Password

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

- **Block user from modifying passcode**: **Yes** stops the passcode from being changed, added, or removed. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passcodes to be added, changed, or removed.

- **Block Touch ID to unlock device**: **Yes** prevents using fingerprints to unlock devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to unlock the device using a fingerprint.

- **Block password AutoFill**: **Yes** prevents using the AutoFill Passwords feature on macOS. Choosing **Yes** also has the following impact:

  - Users aren't prompted to use a saved password in Safari or in any apps.
  - Automatic Strong Passwords are disabled, and strong passwords aren't suggested to users.

  When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these features.

- **Block password proximity requests**: **Yes** prevents devices from requesting passwords from nearby devices. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow these password requests.

- **Block password sharing**: **Yes** prevents sharing passwords between devices using AirDrop. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passwords to be shared.

## Restricted apps

### Settings apply to: All enrollment types

- **Type of restricted apps list**: Create a list of apps that users aren't allowed to install or use. Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, users might have access to apps you assign, and built-in apps.
  - **Approved apps**: List the apps that users are allowed to install. To stay compliant, users must not install other apps. Apps that are managed by Intune are automatically allowed, including the Company Portal app. Users aren't prevented from installing an app that isn't on the approved list. But if they do, it's reported in Intune.
  - **Prohibited apps**: List the apps (not managed by Intune) that users aren't allowed to install and run. Users aren't prevented from installing a prohibited app. If a user installs an app from this list, it's reported in Intune.

- **Apps list**: **Add** apps to your list:
  - **App Bundle ID**: Enter the [bundle ID](bundle-ids-built-in-ios-apps.md) of the app. You can add built-in apps and line-of-business apps. Apple's web site has a list of [built-in Apple apps](https://support.apple.com/HT208094).

    To find the URL of an app, open the iTunes App Store, and search for the app. For example, search for `Microsoft Remote Desktop` or `Microsoft Word`. Select the app, and copy the URL. You can also use iTunes to find the app, and then use the **Copy Link** task to get the app URL.

  - **App name**: Enter a user-friendly name to help you identify the bundle ID. For example, enter `Intune Company Portal app`.
  - **Publisher**: Enter the publisher of the app.

- **Import** a CSV file with details about the app, including the URL. Use the `<app bundle ID>, <app name>, <app publisher>` format. Or, **Export** to create a list of apps you added, in the same format.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also restrict device features and settings on [iOS/iPadOS](device-restrictions-ios.md) devices.
