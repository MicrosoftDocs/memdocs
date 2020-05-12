---
# required metadata

title: Add custom settings to macOS devices in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Export macOS settings from Apple Configurator or Apple Profile Manager tools, and then import these settings into Microsoft Intune. These settings can create, use, and control custom settings and features on macOS devices. This custom profile can then be assigned or distributed to macOS devices in your organization to create a baseline or standard.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
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
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use custom settings for macOS devices in Microsoft Intune

Using Microsoft Intune, you can add or create custom settings for your macOS devices using a "custom profile". Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

When using macOS devices, there are two ways to get custom settings into Intune:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple Profile Manager](https://support.apple.com/profile-manager)

You can use these tools to export settings to a configuration profile. In Intune, you import this file, and then assign the profile to your macOS users and devices. Once assigned, the settings are distributed. They also create a baseline or standard for macOS in your organization.

This article provides some guidance on using Apple Configurator and Apple Profile Manager, and describes the properties you can configure.

## Before you begin

[Create the profile](custom-settings-configure.md).

## What you need to know

- When using **Apple Configurator** to create the configuration profile, be sure the settings you export are compatible with the macOS version on the devices. For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

- When using **Apple Profile Manager**, be sure to:

  - Enable [mobile device management](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) in Profile Manager.
  - Add [macOS devices](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) in Profile Manager.
  - After you add a device in Profile Manager, go to **Under the Library** > **Devices** > select your device > **Settings**. Enter the general, security, privacy, directory, and certificate settings for the device.

    Download and save this file. You'll enter this file in the Intune profile. 

  - Be sure the settings you export from the Apple Profile Manager are compatible with the macOS version on the devices. For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

## Custom configuration profile settings

- **Custom configuration profile name**: Enter a name for the policy. This name is shown on the device, and in the Intune status.
- **Configuration profile file**: Browse to the configuration profile you created using the Apple Configurator or Apple Profile Manager. The file you imported is shown in the **File contents** area.

  You can also add device tokens to your `.mobileconfig` files. Device tokens are used to add device-specific information. For example, to show the serial number, enter `{{serialnumber}}`. On the device, the text shows similar to `123456789ABC`, which is unique to each device. When entering variables, be sure to use curly brackets `{{ }}`. [App configuration tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) includes a list of variables that can be used. You can also use `deviceid` or any other device-specific value.

  > [!NOTE]
  > Variables aren't validated in the UI, and are case sensitive. As a result, you may see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}` instead of `{{deviceid}}`, then the literal string is shown instead of the device's unique ID. Be sure to enter the correct information.

## Next steps

The profile is created, but it may not be doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Create a [custom profile on iOS/iPadOS devices](custom-settings-ios.md).
