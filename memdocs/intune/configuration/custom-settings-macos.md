---
# required metadata

title: Add custom settings to macOS devices in Microsoft Intune
titleSuffix:
description: Import custom macOS settings into Microsoft Intune. These settings can create, use, and control custom settings and features on macOS devices. This custom profile can then be assigned or distributed to macOS devices in your organization to create a baseline or standard.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/28/2024
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

# Use custom settings for macOS devices in Microsoft Intune

> [!IMPORTANT]
> Don't use custom configuration profiles for sensitive information, such as Wi-Fi connections or authenticating apps, websites, and more. Instead, use the built-in profiles for sensitive information, as they're designed and configured to handle sensitive information.
>
> For example, use the built-in [Wi-Fi profile](wi-fi-settings-configure.md) to deploy a Wi-Fi connection. Use the built-in [certificates profile](../protect/certificates-configure.md) for authentication.

Using Microsoft Intune, you can add or create custom settings for your macOS devices using a **custom profile**. Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune. These settings must be in an `.xml` or `.mobileconfig` file.

The Intune settings catalog has many macOS settings, and more are continually added. Before you create a custom profile, look for the settings in the [Settings Catalog](../configuration/settings-catalog.md). It's possible you don't need a custom profile.

This feature applies to:

- macOS

## Before you begin

- Create a [macOS custom device configuration profile](custom-settings-configure.md).

- To create the policy, at a minimum, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an account that has the **Policy and Profile Manager** Intune role. For more information, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

- You might be able to use **Apple Configurator** to export existing macOS settings to an `.xml` or `.mobileconfig` file. Apple Configurator is designed for the iOS/iPadOS platform, not the macOS platform. Make sure the settings you export are compatible with the macOS version on the devices. For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

- For information on Apple's device management and payload keys, go to:

  - [Apple Device Management](https://developer.apple.com/documentation/devicemanagement) (opens Apple's web site)
  - [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's web site)

## Custom configuration profile settings

When you configure the profile, enter the following settings:

- **Configuration profile name**: Enter a name for the policy. This name is shown on the device, and in the Intune status in the Intune admin center.
- **Deployment channel**: Select the channel you want to use to deploy your configuration profile. If you send the profile to the wrong channel, deployment can fail. After you select a channel and save the profile, the channel can't be changed. To select a different channel, create a new profile.

  User-targeted payloads don't apply to devices enrolled without user affinity. For more information on whether a payload can be used for a device configuration profile or a user configuration profile, go to [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's developer website).

- **Configuration profile file**: Browse to the `.xml` or `.mobileconfig` file you created. The max file size is `1000000` bytes (just under 1 MB). The imported file is shown. You can also **Remove** a file after it's been added.

  You can also add device tokens to your `.mobileconfig` files. Device tokens are used to add device-specific information. For example, to show the serial number, enter `{{serialnumber}}`. On the device, the text shows similar to `123456789ABC`, which is unique to each device. When entering variables, be sure to use curly brackets `{{ }}`.

  [App configuration tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) includes a list of variables that can be used. You can also use `deviceid` or any other device-specific value.

  > [!NOTE]
  > Variables aren't validated in the UI, and are case sensitive. As a result, you may see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}` instead of `{{deviceid}}`, then the literal string is shown instead of the device's unique ID. Be sure to enter the correct information.

## Related content

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- Create a [custom profile on iOS/iPadOS devices](custom-settings-ios.md).
