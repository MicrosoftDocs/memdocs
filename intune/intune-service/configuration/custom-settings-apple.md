---
title: Add custom settings to Apple devices in Microsoft Intune
description: Export iOS, iPadOS, and macOS settings from Apple Configurator or Apple Profile Manager tools, and then import these settings into Microsoft Intune. These settings can create, use, and control custom settings and features on iOS, iPadOS, and macOS devices. This custom profile can then be assigned or distributed to iOS, iPadOS, and macOS devices in your organization to create a baseline or standard.
ms.date: 02/05/2026
ms.topic: article
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
zone_pivot_groups: platforms-apple
---

# Use custom settings for Apple devices in Microsoft Intune

Using Microsoft Intune, you can add or create custom settings for your iOS/iPadOS and macOS devices using **custom profiles**. Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

This article describes the properties you can configure and provides some guidance on the Apple tools, like Apple Configurator.

[!INCLUDE [settings-catalog-more-settings](../includes/settings-catalog-more-settings.md)] It's possible you don't need a custom profile.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> This feature supports the following platforms:
>
> - iOS/iPadOS
> - macOS
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> - Create a [VPN device configuration profile](vpn-settings-configure.md).
:::column-end:::
:::row-end:::

## Before you begin

- Don't use custom configuration profiles for sensitive information, such as Wi-Fi connections or authenticating apps, sites, and more. Instead, use the built-in profiles for sensitive information, as they're designed and configured to handle sensitive information.

  For example, use the built-in [Wi-Fi profile](wi-fi-settings-configure.md) to deploy a Wi-Fi connection. Use the built-in [certificates profile](../protect/certificates-configure.md) for authentication.

::: zone pivot="ios-ipados"

- When you use iOS/iPadOS devices, there are tools to help you get custom settings into Intune:

  - [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344) (opens Apple's website)
  - [Apple Profile Manager](https://support.apple.com/guide/server/intro-to-profile-manager-apd0e2214c6/5.12/mac) (opens Apple's website)

  You can use these tools to export settings to a configuration profile. In Intune, you import this file, and then assign the profile to your iOS/iPadOS users and devices. Once assigned, the settings are distributed. They also create a baseline or standard for iOS/iPadOS in your organization.

::: zone-end

::: zone pivot="macos"

- For macOS devices, the settings must be in an `.xml` or `.mobileconfig` file.

  You might be able to use **Apple Configurator** to export existing macOS settings to an `.xml` or `.mobileconfig` file. Apple Configurator is designed for the iOS/iPadOS platform, not the macOS platform. So, make sure the settings you export are compatible with the macOS version on the devices.

  For information on resolving incompatible settings, search for **Configuration Profile Reference** and **Mobile Device Management Protocol Reference** on the [Apple Developer](https://developer.apple.com/) website.

::: zone-end

- For information on Apple's device management and payload keys, go to:

  - [Apple Device Management](https://developer.apple.com/documentation/devicemanagement) (opens Apple's web site)
  - [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's web site)

## Custom configuration profile settings

When you configure the profile, enter the following settings:

::: zone pivot="ios-ipados"

- **Custom configuration profile name**: Enter a name for the policy. The device and Intune status show this name.
- **Configuration profile file**: Browse to the configuration profile you created by using the Apple Configurator or Apple Profile Manager. The max file size is `1000000` bytes (just under 1 MB). The **File contents** area shows the imported file.

  You can also add device tokens to your custom configuration files. Use device tokens to add device-specific information. For example, to show the serial number, enter `{{serialnumber}}`. On the device, the text shows similar to `123456789ABC`, which is unique to each device.

  When entering variables, be sure to use curly brackets `{{ }}`. [App configuration tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) includes a list of variables that you can use. You can also use `deviceid` or any other device-specific value.

::: zone-end

::: zone pivot="macos"

- **Configuration profile name**: Enter a name for the policy. This name is shown on the device, and in the Intune status in the Intune admin center.
- **Deployment channel**: Select the channel you want to use to deploy your configuration profile. If you send the profile to the wrong channel, deployment can fail. After you select a channel and save the profile, you can't change the channel. To select a different channel, create a new profile.

  User-targeted payloads don't apply to devices enrolled without user affinity. For more information on whether a payload can be used for a device configuration profile or a user configuration profile, see [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple's developer website).

- **Configuration profile file**: Browse to the `.xml` or `.mobileconfig` file you created. The max file size is `1000000` bytes (just under 1 MB). The imported file is shown. You can also **Remove** a file after you add it.

  You can also add device tokens to your `.mobileconfig` files. Use device tokens to add device-specific information. For example, to show the serial number, enter `{{serialnumber}}`. On the device, the text shows similar to `123456789ABC`, which is unique to each device. When entering variables, be sure to use curly brackets `{{ }}`.

  [App configuration tokens](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) includes a list of variables that can be used. You can also use `deviceid` or any other device-specific value.

::: zone-end

> [!NOTE]
> The UI doesn't validate variables, and they're case sensitive. As a result, you might see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}` instead of `{{deviceid}}`, the literal string shows instead of the device's unique ID. Be sure to enter the correct information.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- Learn about [custom profiles](custom-settings-configure.md).
