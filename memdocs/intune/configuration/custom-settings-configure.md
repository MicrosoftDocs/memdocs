---
# required metadata

title: Use custom device settings in Microsoft Intune - Azure | Microsoft Docs
description: Add or create a profile to use custom settings for Windows Phone, Windows 8.1, Windows 10 and later, Android, Android Enterprise, macOS, and iOS/iPadOS devices using Microsoft Intune
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
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

# Create a profile with custom settings in Intune

## What are custom profiles

Microsoft Intune includes many built-in settings to control different features on a device. You can also create custom profiles. Custom profiles are great when you want to use device settings and features that aren't built in to Intune. These profiles include features and settings for you to control on devices in your organization. For example, you can create a custom profile that sets the same feature for every iOS/iPadOS device.

For more information on configuration profiles, see [What are Microsoft Intune device profiles?](device-profiles.md). 

This article includes links to create custom profiles for Android, Android Enterprise, iOS/iPadOS, macOS, and Windows.

## Available platforms

Custom settings are configured differently for each platform. For example, to control features on Android and Windows devices, you can enter Open Mobile Alliance Uniform Resource Identifier (OMA-URI) values. For Apple devices, you can import a file you created with the [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) or [Apple Profile Manager](https://support.apple.com/profile-manager).

Custom profiles are created similar to built-in profiles, and are available on the following platforms:

- [Android](../custom-settings-android.md)
- [Android Enterprise](../custom-settings-android-for-work.md)
- [iOS/iPadOS](custom-settings-ios.md)
- [macOS](custom-settings-macos.md)
- [Windows 10](custom-settings-windows-10.md)
- [Windows Holographic for Business](custom-settings-windows-holographic.md)
- [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

## Next steps

Choose your platform, and get started:

- [Android](../custom-settings-android.md)
- [Android Enterprise](../custom-settings-android-for-work.md)
- [iOS/iPadOS](custom-settings-ios.md)
- [macOS](custom-settings-macos.md)
- [Windows 10](custom-settings-windows-10.md)
- [Windows Holographic for Business](custom-settings-windows-holographic.md)
- [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)
