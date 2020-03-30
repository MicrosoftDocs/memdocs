---
# required metadata

title: Add custom settings to iOS/iPadOS devices in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Export iOS and iPadOS settings from Apple Configurator or Apple Profile Manager tools, and then import these settings into Microsoft Intune. These settings can create, use, and control custom settings and features on iOS/iPadOS devices. This custom profile can then be assigned or distributed to iOS/iPadOS devices in your organization to create a baseline or standard.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/25/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
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

# Use custom settings for iOS and iPadOS devices in Microsoft Intune

Using Microsoft Intune, you can add or create custom settings for your iOS/iPadOS devices using "custom profiles". Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

When using iOS/iPadOS devices, there are two ways to get custom settings into Intune:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple Profile Manager](https://support.apple.com/profile-manager)

You can use these tools to export settings to a configuration profile. In Intune, you import this file, and then assign the profile to your iOS/iPadOS users and devices. Once assigned, the settings are distributed. They also create a baseline or standard for iOS/iPadOS in your organization.

This article provides some guidance on using Apple Configurator and Apple Profile Manager, and describes the properties you can configure.

## Before you begin

[Create the profile](custom-settings-configure.md).

## What you need to know

- When using **Apple Configurator** to create the configuration profile, be sure the settings you export are compatible with the iOS/iPadOS version on the devices. For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

- When using **Apple Profile Manager**, be sure to:

  - Enable [mobile device management](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) in Profile Manager.
  - Add [iOS/iPadOS devices](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) in Profile Manager.
  - After you add a device in Profile Manager, go to **Under the Library** > **Devices** > select your device > **Settings**. Enter the general settings for the device.

    Download and save this file. You'll enter this file in the Intune profile.

  - Be sure the settings you export from the Apple Profile Manager are compatible with the iOS/iPadOS version on the devices. For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

## Custom configuration profile settings

- **Custom configuration profile name**: Enter a name for the policy. This name is shown on the device, and in the Intune status.
- **Configuration profile file**: Browse to the configuration profile you created using the Apple Configurator or Apple Profile Manager. The max file size is `1000000` bytes (just under 1MB). The file you imported is shown in the **File contents** area.

  You can also add device tokens to your custom configuration files. Device tokens are used to add device-specific information. For example, to show the serial number, enter `{{serialnumber}}`. On the device, the text shows similar to `123456789ABC`, which is unique to each device. When entering variables, be sure to use curly brackets `{{ }}`. [App configuration tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) includes a list of variables that can be used. You can also use `deviceid` or any other device-specific value.

  > [!NOTE]
  > Variables aren't validated in the UI, and are case sensitive. As a result, you may see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}` instead of `{{deviceid}}`, then the literal string is shown instead of the device's unique ID. Be sure to enter the correct information.

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](device-profile-assign.md).

See how to [create the profile on macOS devices](custom-settings-macos.md). 
