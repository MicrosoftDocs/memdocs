---
# required metadata

title: Add custom settings to iOS/iPadOS devices in Microsoft Intune
titleSuffix:
description: Export iOS and iPadOS settings from Apple Configurator or Apple Profile Manager tools, and then import these settings into Microsoft Intune. These settings can create, use, and control custom settings and features on iOS/iPadOS devices. This custom profile can then be assigned or distributed to iOS/iPadOS devices in your organization to create a baseline or standard.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use custom settings for iOS and iPadOS devices in Microsoft Intune

> [!IMPORTANT]
> Don't use custom configuration profiles for sensitive information, such as Wi-Fi connections or authenticating apps, sites, and more. Instead, use the built-in profiles for sensitive information, as they're designed and configured to handle sensitive information.
>
> For example, use the built-in [Wi-Fi profile](wi-fi-settings-configure.md) to deploy a Wi-Fi connection. Use the built-in [certificates profile](../protect/certificates-configure.md) for authentication.

Using Microsoft Intune, you can add or create custom settings for your iOS/iPadOS devices using **custom profiles**. Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

This feature applies to:

- iOS/iPadOS

When you use iOS/iPadOS devices, there are two ways to get custom settings into Intune:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344) (opens Apple's website)
- [Apple Profile Manager](https://support.apple.com/guide/server/intro-to-profile-manager-apd0e2214c6/5.12/mac) (opens Apple's website)

You can use these tools to export settings to a configuration profile. In Intune, you import this file, and then assign the profile to your iOS/iPadOS users and devices. Once assigned, the settings are distributed. They also create a baseline or standard for iOS/iPadOS in your organization.

This article provides some guidance on using Apple Configurator and Apple Profile Manager, and describes the properties you can configure.

## Before you begin

- Create an [iOS/iPadOS custom device configuration profile](custom-settings-configure.md).
- [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]

## What you need to know

- When using **Apple Configurator** to create the configuration profile, be sure the settings you export are compatible with the iOS/iPadOS version on the devices. For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

- When using **Apple Profile Manager**, be sure to:

  - In Apple Profile Manager, enable [mobile device management](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C).
  - In Apple Profile Manager, add [iOS/iPadOS devices](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984).
  - After you add a device in Apple Profile Manager, go to **Under the Library** > **Devices** > select your device > **Settings**. Enter the general settings for the device.

    Download and save this file. You enter this file in the Intune profile.

  - Be sure the settings you export from the Apple Profile Manager are compatible with the iOS/iPadOS version on the devices. For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

## Custom configuration profile settings

When you configure the profile, enter the following settings:

- **Custom configuration profile name**: Enter a name for the policy. This name is shown on the device, and in the Intune status.
- **Configuration profile file**: Browse to the configuration profile you created using the Apple Configurator or Apple Profile Manager. The max file size is `1000000` bytes (just under 1 MB). The imported file is shown in the **File contents** area.

  You can also add device tokens to your custom configuration files. Device tokens are used to add device-specific information. For example, to show the serial number, enter `{{serialnumber}}`. On the device, the text shows similar to `123456789ABC`, which is unique to each device.

  When entering variables, be sure to use curly brackets `{{ }}`. [App configuration tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) includes a list of variables that can be used. You can also use `deviceid` or any other device-specific value.

  > [!NOTE]
  > Variables aren't validated in the UI, and are case sensitive. As a result, you can see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}` instead of `{{deviceid}}`, then the literal string is shown instead of the device's unique ID. Be sure to enter the correct information.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- [Create custom profiles on macOS devices](custom-settings-macos.md).
