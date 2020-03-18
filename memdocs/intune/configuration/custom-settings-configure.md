---
# required metadata

title: Use custom device settings in Microsoft Intune - Azure | Microsoft Docs
description: Add or create a profile to use custom settings for Windows Phone, Windows 8.1, Windows 10 and later, Android device administrator, Android Enterprise, macOS, and iOS/iPadOS devices using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Create a profile with custom settings in Intune

Microsoft Intune includes many built-in settings to control different features on a device. You can also create custom profiles, which are created similar to built-in profiles. Custom profiles are great when you want to use device settings and features that aren't built in to Intune. These profiles include features and settings for you to control on devices in your organization. For example, you can create a custom profile that sets the same feature for every iOS/iPadOS device.

Custom settings are configured differently for each platform. For example, to control features on Android and Windows devices, you can enter Open Mobile Alliance Uniform Resource Identifier (OMA-URI) values. For Apple devices, you can import a file you created with the [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) or [Apple Profile Manager](https://support.apple.com/profile-manager).

For more information on configuration profiles, see [What are Microsoft Intune device profiles?](device-profiles.md).

This article shows you how to create a custom profile for Android device administrator, Android Enterprise, iOS/iPadOS, macOS, and Windows. You can also see all the available settings for the different platforms.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Windows 10: Custom profile that enables AllowVPNOverCellular custom OMA-URI**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Platform**: Select the platform of your devices. Your options:

      - **Android device administrator**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 and later**
      - **Windows 8.1 and later**

    - **Profile Type**: Select **Custom**.

4. The settings are different for each platform. To see the settings for a specific platform, select your platform:

    - [Android device administrator](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. When you're done, select **Create Profile** > **Create**.

The profile is created, and shown in the profiles list (**Device configuration** > **Profiles**).

## Next steps

After the profile is created, it's ready to be assigned. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
