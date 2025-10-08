---
title: iOS/iPadOS supervised device security configurations
description: Review example supervised device security configurations of basic, enhanced, and high security for iOS devices.
author: brenduns
ms.author: brenduns
ms.date: 03/20/2025
ms.topic: reference
ms.reviewer:
ms.collection:
- M365-identity-device-management
- highpri
---

# iOS/iPadOS supervised device security configurations examples

In support of the [Microsoft Zero Trust security model](/security/zero-trust/zero-trust-identity-device-access-policies-common), this article provides example configurations you can use with Microsoft Intune to configure iOS/iPad device compliance settings for mobile users using supervised devices. These examples include three levels of device security configuration that align with Zero Trust principles.

When using these examples, work with your security team to evaluate the threat environment, risk appetite, and the effect the different levels and configurations can have on usability. After reviewing and adjusting the examples to meet the needs of your organization, you can incorporate them within a ring deployment methodology for testing and production use by importing the sample [iOS/iPadOS Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/iOS) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

For more information on each policy setting, see [iOS/iPadOS device settings in Microsoft Intune](../configuration/device-restrictions-ios.md).

## Supervised basic security (level 1)

Level 1 is the minimum security configuration for an enterprise mobile device owned by the organization.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users by:

- Enforcing password policies.
- Enabling certain device lock characteristics.
- Disabling certain device functions (like untrusted certificates).

The following table lists only configured settings. Settings not listed in the table aren't configured in this example.

### Device restrictions

| Category | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Treat AirDrop as an unmanaged destination | Yes |  |
| Built-in Apps | Block Siri while device is locked | Yes |  |
| Built-in Apps | Require Safari fraud warnings  | Yes |  |
| Cloud and Storage | Force encrypted backup | Yes |  |
| Cloud and Storage | Block managed apps from storing data in iCloud | Yes |  |
| Cloud and Storage | Block iCloud Keychain sync | Yes |  |
| Connected Devices | Force Apple Watch wrist detection | Yes |  |
| Connected Devices | Block storage of AirPrint credentials in Keychain | Yes |  |
| Connected Devices | Require AirPrint to destinations with trusted certificates | Yes |  |
| Connected Devices | Block iBeacon discovery of AirPrint printers | Yes |  |
| Connected Devices | Block setting up new nearby devices  | Yes |  |
| General | Block untrusted TLS certificates | Yes |  |
| General | Block trusting new enterprise app authors | Yes |  |
| General | Allow activation lock | Yes |  |
| Locked Screen Experience | Block Notification Center access in lock screen | Yes |  |
| Locked Screen Experience | Block Today view in lock screen | Yes |  |
| Password | Require a password | Yes |  |
| Password | Block simple passwords | Yes |  |
| Password | Required password type | Numeric |  |
| Password | Minimum password length | 6 | Organizations should update this setting to match their password policy. |
| Password | Number of sign-in failures before wiping the device | 10 | Organizations should update this setting to match their password policy. |
| Password | Maximum minutes after screen lock before password is required | 5 | Organizations should update this setting to match their password policy. |
| Password | Maximum minutes of inactivity until screen locks  | 5 | Organizations should update this setting to match their password policy. |
| Password | Block password proximity requests | Yes |  |
| Password | Block password sharing | Yes |  |
| Password | Require Touch ID or Face ID authentication for AutoFill of password or credit card information | Yes |  |

## Supervised enhanced security (level 2)

Level 2 is the recommended configuration for supervised devices where users access more sensitive information. These devices are a natural target in enterprises today. These settings don't assume a large staff of highly skilled security personnel. Therefore, they should be accessible to most enterprise organizations. This configuration is applicable to most mobile users accessing work or school data on a device.

This configuration expands upon the configuration in Level 1 by enacting data transfer controls and blocking access to USB devices.

The level 2 settings include all the policy settings recommended for level 1. However, the settings listed in the following table include only those settings that are added or changed. These settings can have a slightly higher impact to users or to applications. They enforce a level of security more appropriate for risks facing users with access to sensitive information on mobile devices.

### Device restrictions

| Category | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Block viewing corporate documents in unmanaged apps | Yes |  |
| App Store, Doc Viewing, Gaming | Block viewing non-corporate documents in corporate apps | Not configured | Enabling this device restriction blocks Outlook for iOS’s ability to export contacts. This setting isn't recommended if using Outlook for iOS. For more information, see [Support Tip: Enabling Outlook iOS Contact Sync with iOS12 MDM Controls](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-enabling-outlook-ios-contact-sync-with-ios12-mdm/ba-p/298453). |
| App Store, Doc Viewing, Gaming | Allow managed apps to write contacts to unmanaged contacts accounts | Yes | This setting is needed to allow Outlook for iOS to export contacts when **Block viewing corporate documents in unmanaged apps** is set to *Yes*. For more information, see [Support Tip: Enabling Outlook iOS Contact Sync with iOS12 MDM Controls](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-enabling-outlook-ios-contact-sync-with-ios12-mdm/ba-p/298453). |
| App Store, Doc Viewing, Gaming | Allow copy/paste to be affected by managed open-in | Yes | Enabling this setting blocks personal accounts within managed Microsoft apps from sharing data to unmanaged apps. |
| Built-in Apps | Block Siri for dictation   | Yes |  |
| Built-in Apps | Block Siri for translation   | Yes |  |
| Cloud Storage | Block backup of enterprise books | Yes |  |
| Cloud Storage | Block notes and highlights sync for enterprise books | Yes |  |
| Cloud Storage | Block iCloud document and data sync | Yes |  |
| Connected Devices | Block access to USB in Files app | Yes |  |
| General | Block sending diagnostic and usage data to Apple | Yes |  |

## Supervised high security (level 3)

Level 3 is the recommended configuration for both:

- Organizations with large and sophisticated security organizations.
- Specific users and groups who are uniquely targeted by adversaries.

Such organizations are typically targeted by well-funded and sophisticated adversaries.

This configuration expands upon level 2 by:

- Enacting stronger password policies.
- Disabling device functionality (like AirPrint).
- Requiring app installation through Apple’s volume purchase program. For more information, see [How to manage iOS and macOS apps purchased through Apple Business Manager with Microsoft Intune](../apps/vpp-apps-ios.md).
- Enforcing additional data transfer restrictions (like blocking iCloud backup).

The policy settings enforced in level 3 include all the policy settings recommended for level 2. The settings listed in the following table include only those that are added or changed. These settings can have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations.

### Device restrictions

| Category | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Block App store | Yes |  |
| App Store, Doc Viewing, Gaming | Block playback of explicit music, podcast, and iTunes U | Yes |  |
| App Store, Doc Viewing, Gaming | Block adding Game Center friends | Yes |  |
| App Store, Doc Viewing, Gaming | Block Game Center | Yes |  |
| App Store, Doc Viewing, Gaming | Block multiplayer gaming | Yes |  |
| App Store, Doc Viewing, Gaming | Block access to network drive in Files app | Yes |  |
| Built-in Apps | Block Siri | Yes |  |
| Built-in Apps | Block iTunes store | Yes |  |
| Built-in Apps | Block Find My Friends | Yes |  |
| Built-in Apps | Block user modification to the Find My Friends settings | Yes |  |
| Built-in Apps | Block Safari Autofill | Yes |  |
| Cloud and Storage | Block Handoff | Yes |  |
| Cloud and Storage | Block iCloud backup | Yes |  |
| Connected Devices | Require AirPlay outgoing requests pairing password | Yes |  |
| Connected Devices | Block Apple Watch auto unlock | Yes |  |
| Connected Devices | Block AirDrop | Yes |  |
| Connected Devices | Block pairing with non-Configurator hosts | Yes |  |
| Connected Devices | Block AirPrint | Yes |  |
| Connected Devices | Allow users to boot devices into recovery mode with unpaired devices  | Not configured |  |
| General | Block screenshots and screen recording | Yes |  |
| General | Block modification of account settings | Yes |  |
| General | Block users from erasing all content and settings on device | Yes |  |
| General | Block configuration profile changes | Yes |  |
| General | Block removing apps | Yes |  |
| General | Force automatic data and time | Yes |  |
| General | Block VPN creation | Yes |  |
| General | Block modification of eSIM settings | Yes |  |
| Password | Number of sign-in failures before wiping the device | 5 | Organizations should update this setting to match their password policy. |
| Password | Password expiration (days) | 365 | Organizations should update this setting to match their password policy. |
| Password | Prevent reuse of previous passwords | 5 | Organizations should update this setting to match their password policy. |
| Password | Block password AutoFill | Yes | |
| Wireless | Block voice dialing while device is locked | Yes |  |
| Wireless | Require joining Wi-Fi networks only using configuration profiles | Not configured | Take care when using this setting as it could affect your ability to connect to the device if the specified Wi-Fi Networks are unavailable or if the setting is configured incorrectly. This could result in a situation where you're locked out of the device and unable to remotely reset the device. |

## Related articles

- [Configure device compliance security policies](../protect/ios-ipados-device-compliance-security-configurations.md)
- [Configure device security policies for personal devices](../protect/ios-ipados-personal-device-security-configurations.md)