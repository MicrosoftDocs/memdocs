---
# required metadata

title: macOS device settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add, configure, or create settings on macOS devices to restrict features, including setting password requirements, control the locked screen, use built-in apps, add restricted or approved apps, handle bluetooth devices, connect to the cloud for backup and storage, enable kiosk mode, add domains, and control how users interact with the Safari web browser in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# macOS device settings to allow or restrict features using Intune



This article lists and describes the different settings you can control on macOS devices. As part of your mobile device management (MDM) solution, use these settings to allow or disable features, set password rules, allow or restrict specific apps, and more.

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

## Before you begin

[Create a device restrictions configuration profile](../device-restrictions-configure.md).

> [!NOTE]
> These settings apply to different enrollment types. For more information on the different enrollment types, see [macOS enrollment](../macos-enroll.md).

## General

### Settings apply to: Device enrollment and Automated device enrollment

- **Definition Lookup**: **Block** prevents user from highlighting a word, and then looking up its definition on the device. **Not configured** (default) allows access to the definition lookup feature.
- **Dictation**: **Block** stops the user from using voice input to enter text. **Not configured** (default) allows the user to use dictation input.
- **Content caching**: Choose **Not configured** (default) to enable content caching. Content caching stores app data, web browser data, downloads, and more locally on the device. Select **Block** to prevent this data from being stored in the cache.

  For more information on content caching on macOS, see [Manage content caching on Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (opens another website).

  This feature applies to:  
  - macOS 10.13 and newer

- **Defer software updates**: When set to **Not configured** (default), software updates are shown on the device as Apple releases them. For example, if a macOS update gets released by Apple on a specific date, then that update naturally shows up on the device around the release date. Seed build updates are allowed without delay.

  **Enable** allows you to delay when software updates are shown on devices, from 0-90 days. This setting doesn't control when updates are or aren't installed. 

  - **Delay visibility of software updates**: Enter a value from 0-90 days. When the delay expires, users get a notification to update to the earliest version of the OS available when the delay was triggered.

    For example, if a macOS update is available on **January 1**, and **Delay visibility** is set to **5 days**, then the update isn't shown as an available update. On the **sixth day** following the release, that update is available, and end users can install it.

    This feature applies to:  
    - macOS 10.13.4 and newer

- **Screenshots**: Device must be enrolled in Apple's Automated Device Enrollment (DEP). When set to **Block**, users can't save a screenshot of the display. It also prevents the Classroom app from observing remote screens. **Not configured** (default) allows users to capture screenshots, and allows the Classroom app to view remote screens.

### Settings apply to: Automated device enrollment

- **Remote screen observation through Classroom app**: **Disable** prevents teachers from using the Classroom app to see their students' screens. **Not configured** (default) allows teachers to see their students' screens.

  To use this setting, set the **Screenshots** setting to **Not configured** (screenshots are allowed).

- **Unprompted screen observation by Classroom app**: **Allow** lets teachers see their students’ screens without requiring the student to agree. **Not configured** (default) requires the student to agree before the teacher can see the screens.

  To use this setting, set the **Screenshots** setting to **Not configured** (screenshots are allowed).

- **Students must request permission to leave Classroom class**: **Require** forces students enrolled in an unmanaged Classroom course to get teacher approval to leave the course. **Not configured** (default) allows student to leave the course whenever the student chooses.

- **Teachers can automatically lock devices or apps in the Classroom app**: **Allow** lets teachers lock a student's device or app without the student's approval. **Not configured** (default) requires the student to agree before the teacher can lock the device or app.

- **Students can automatically join Classroom class**: **Allow** lets students join a class without prompting the teacher. **Not configured** (default) requires teacher approval to join a class.

## Password

### Settings apply to: Device enrollment and Automated device enrollment

- **Password**: **Require** the end user to enter a password to access the device. **Not configured** (default) doesn't require a password. It also doesn't force any restrictions, such as blocking simple passwords or setting a minimum length.
  - **Required password type**: Specify whether the password can be Numeric only, or whether it must be Alphanumeric (contain letters and numbers).

    This feature applies to:  
    - macOS 10.10.3 and newer

  - **Number of non-alphanumeric characters in password**: Specify the number of complex characters required in the password (**0** to **4**).<br>A complex character is a symbol, for example "**?**".
  - **Minimum password length**: Enter the minimum length of password a user must configure (between **4** and **16** characters).
  - **Simple passwords**: Allow the use of simple passwords such as **0000** or **1234**.
  - **Maximum minutes after screen lock before password is required**: Specify how long the computer must be inactive before a password is required to unlock it.
  - **Maximum minutes of inactivity until screen locks**: Specify the length of time that the computer must be idle before the screen locks.
  - **Password expiration (days)**: Specify how many days elapse before the user must change the password (**1** to **255** days).
  - **Prevent reuse of previous passwords**: Enter the number of previously used passwords that can't be reused, from **1** to **24**.

- **Block User from Modifying Passcode**: Choose **Block** to stop the passcode from being changed, added, or removed. **Not configured** (default) allows passcodes to be added, changed, or removed.
- **Block Fingerprint Unlock**: Choose **Block** to prevent using a fingerprint to unlock the device. **Not configured** (default) allows the user to unlock the device using a fingerprint.

- **Block password AutoFill**: Choose **Block** to prevent using the AutoFill Passwords feature on macOS. Choosing **Block** also has the following impact:

  - Users aren't prompted to use a saved password in Safari or in any apps.
  - Automatic Strong Passwords are disabled, and strong passwords aren't suggested to users.

  **Not configured** (default) allows these features.

- **Block password proximity requests**: Choose **Block** so a user’s device doesn't request passwords from nearby devices. **Not configured** (default) allows these password requests.

- **Block password sharing**: **Block** prevents sharing passwords between devices using AirDrop. **Not configured** (default) allows passwords to be shared.

## Built-in Apps

### Settings apply to: Device enrollment and Automated device enrollment

- **Block Safari AutoFill**: **Block** disables the autofill feature in Safari on the device. **Not configured** (default) allows users to change autocomplete settings in the web browser.
- **Block Camera**: Choose **Block** to prevent access to the camera on the device. **Not configured** (default) allows access to the device's camera.
- **Block Apple Music**: **Block** reverts the Music app to classic mode and disables the Music service. **Not configured** (default) allows using the Apple Music app.
- **Block Spotlight Internet Search Results**: **Block** stops Spotlight from returning any results from an Internet search. **Not configured** (default) allows Spotlight search connect to the Internet to provide search results.
- **Block File Transfer using iTunes**: **Block** disables application file sharing services. **Not configured** (default) allows application file sharing services.

  This feature applies to:  
  - macOS 10.13 and newer

## Restricted apps

### Settings apply to: Device enrollment and Automated device enrollment

- **Type of restricted apps list**: Create a list of apps that users aren't allowed to install or use. Your options:

  - **Not configured** (default): There are no restrictions from Intune. Users have access to apps you assign, and built-in apps.
  - **Prohibited apps**: Apps not managed by Intune that you don't want installed on the device. Users aren't prevented from installing a prohibited app. But if a user installs an app from this list, it's reported in Intune.
  - **Approved apps**: Apps that users are allowed to install. Users must not install apps that aren't listed. Apps that are managed by Intune are automatically allowed. Users aren't prevented from installing an app that isn't on the approved list. But if they do, it's reported in Intune.
- **App Bundle ID**: Enter the app [bundle ID](bundle-ids-built-in-ios-apps.md) of the app you want. You can show or hide built-in apps and line-of-business apps. Apple's web site has a list of [built-in Apple apps](https://support.apple.com/HT208094).
- **App name**: Enter the app name of the app you want. You can show or hide built-in apps and line-of-business apps. Apple's web site has a list of [built-in Apple apps](https://support.apple.com/HT208094).
- **Publisher**: Enter the publisher of the app you want.

To add apps to these lists, you can:

- **Add**: Select to create your list of apps.
- **Import** a CSV file with details about the app, including the URL. Use the `<app bundle ID>, <app name>, <app publisher>` format. Or, **Export** to create a list of apps you added, in the same format.

## Connected devices

### Settings apply to: Device enrollment and Automated device enrollment

- **Block AirDrop**: **Block** prevents using AirDrop on the device. **Not configured** (default) allows using the AirDrop feature to exchange content with nearby devices.
- **Block Apple Watch Auto Unlock**: **Block** prevents users from unlocking their macOS device with their Apple Watch. **Not configured** (default) allows users to unlock their macOS device with their Apple Watch.

## Cloud and storage

### Settings apply to: Device enrollment and Automated device enrollment

- **Block iCloud Keychain sync**: Choose **Block** to disable syncing credentials stored in the Keychain to iCloud. **Not configured** (default) allows users to sync these credentials.
- **Block iCloud Document Sync**: **Block** prevents iCloud from syncing documents and data. **Not configured** (default) allows document and key-value synchronization to your iCloud storage space.
- **Block iCloud Mail Backup**: **Block** prevents iCloud from syncing to the macOS Mail app. **Not configured** (default) allows Mail synchronization to iCloud.
- **Block iCloud Contact Backup**: **Block** prevents iCloud from syncing the devices contacts. **Not configured** (default) allows contact sync using iCloud.
- **Block iCloud Calendar Backup**: **Block** prevents iCloud from syncing to the macOS Calendar app. **Not configured** (default) allows Calendar synchronization to iCloud.
- **Block iCloud Reminder Backup**: **Block** prevents iCloud from syncing to the macOS Reminders app. **Not configured** (default) allows Reminders synchronization to iCloud.
- **Block iCloud Bookmark Backup**: **Block** prevents iCloud from syncing the devices Bookmarks. **Not configured** (default) allows Bookmark synchronization to iCloud.
- **Block iCloud Notes Backup**: **Block** prevents iCloud from syncing the devices Notes. **Not configured** (default) allows Notes synchronization to iCloud.
- **Block iCloud Photo Library**: **Block** disables iCloud Photo Library, and prevents iCloud from syncing the devices photos. Any photos not fully downloaded from iCloud Photo Library are removed from local storage on the device. **Not configured** (default) allows syncing photos between the device and the iCloud Photo Library.
- **Handoff**: **Not configured** (default) allows users to start work on a macOS device, and then continue the work they started on another iOS/iPadOS or macOS device. **Block** prevents the Handoff feature on the device. 

  This feature applies to:  
  - macOS 10.15 and newer

## Domains

### Settings apply to: Device enrollment and Automated device enrollment

- **Email Domain URL**: **Add** one or more URLs to the list. When users receive an email from a domain other than one you configured, the email is marked as untrusted in the macOS Mail app.

## Next steps

[Assign the profile](../device-profile-assign.md) and [monitor its status](../device-profile-monitor.md).

You can also restrict device features and settings on [iOS/iPadOS](../device-restrictions-ios.md) devices.
