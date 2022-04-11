---
# required metadata

title: iOS/iPadOS supervised device security configurations
titleSuffix: Microsoft Intune
description: Learn the settings suggested for iOS/iPadOS supervised device basic and high security.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/01/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
---

# iOS/iPadOS supervised device security configurations

As part of the [iOS/iPadOS security configuration framework](ios-ipados-configuration-framework.md), apply the following device compliance settings to mobile users using supervised devices. For more information on each policy setting, see [iOS/iPadOS device settings in Microsoft Intune](../configuration/device-restrictions-ios.md).

When choosing your settings, be sure to review and categorize usage scenarios. Then, configure users following the guidance for the chosen security level. You can adjust the suggested settings based on the needs of your organization. Make sure to have your security team evaluate the threat environment, risk appetite, and impact to usability.

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [iOS/iPadOS Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/iOS) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

## Supervised basic security (Level 1)

Level 1 is the minimum security configuration for an enterprise mobile device owned by the organization.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users by:

- Enforcing password policies.
- Enabling certain device lock characteristics.
- Disabling certain device functions (like untrusted certificates).

To simplify the table below, only configured settings are listed. Undocumented device restrictions are not configured.

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Treat AirDrop as an unmanaged destination | Yes ||
| Built-in Apps | Block Siri while device is locked | Yes ||
| Built-in Apps | Require Safari fraud warnings  | Yes ||
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
| Password | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| Password | Number of sign-in failures before wiping the device | 10 | Organizations may need to update this setting to match their password policy. |
| Password | Maximum minutes after screen lock before password is required | 5 | Organizations may need to update this setting to match their password policy. |
| Password | Maximum minutes of inactivity until screen locks  | 5 | Organizations may need to update this setting to match their password policy. |
| Password | Block password proximity requests | Yes |  |
| Password | Block password sharing | Yes |  |
| Password | Require Touch ID or Face ID authentication for AutoFill of password or credit card information | Yes |  |

## Supervised enhanced security (Level 2)

Level 2 is the recommended configuration for supervised  devices where users access more sensitive information. These devices are a natural target in enterprises today. These settings don't assume a large staff of highly skilled security personnel. Therefore, they should be accessible to most enterprise organizations. This configuration is applicable to most mobile users accessing work or school data on a device.

This configuration expands upon the configuration in Level 1 by enacting data transfer controls and blocking access to USB devices.

The level 2 settings include all the policy settings recommended for level 1. However, the settings listed below include only those settings that have been added or changed. These settings may have a slightly higher impact to users or to applications. They enforce a level of security more appropriate for risks facing users with access to sensitive information on mobile devices.

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Block viewing corporate documents in unmanaged apps | Yes ||
| App Store, Doc Viewing, Gaming | Block viewing non-corporate documents in corporate apps | Not configured | Enabling this device restriction blocks Outlook for iOS’s ability to export contacts. This setting is not recommended if using Outlook for iOS. For more information, see [Support Tip: Enabling Outlook iOS Contact Sync with iOS12 MDM Controls](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-enabling-outlook-ios-contact-sync-with-ios12-mdm/ba-p/298453). |
| App Store, Doc Viewing, Gaming | Allow managed apps to write contacts to unmanaged contacts accounts | Yes | This setting is needed to allow Outlook for iOS to export contacts when **Block viewing corporate documents in unmanaged apps** is set to *Yes*. For more information, see [Support Tip: Enabling Outlook iOS Contact Sync with iOS12 MDM Controls](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-enabling-outlook-ios-contact-sync-with-ios12-mdm/ba-p/298453). |
| App Store, Doc Viewing, Gaming | Allow copy/paste to be affected by managed open-in | Yes | Enabling this setting will block personal accounts within managed Microsoft apps from sharing data to unmanaged apps. |
| Built-in Apps | Block Siri for dictation   | Yes ||
| Built-in Apps | Block Siri for translation   | Yes ||
| Cloud Storage | Block backup of enterprise books | Yes |  |
| Cloud Storage | Block notes and highlights sync for enterprise books | Yes |  |
| Cloud Storage | Block iCloud document and data sync | Yes |  |
| Connected Devices | Block access to USB in Files app | Yes |  |
| General | Block sending diagnostic and usage data to Apple | Yes |  |

## Supervised high security (Level 3)

Level 3 is the recommended configuration for both:

- Organizations with large and sophisticated security organizations.
- Specific users and groups who will be uniquely targeted by adversaries. Such organizations are typically targeted by well-funded and sophisticated adversaries.

This configuration expands upon Level 2 by:

- Enacting stronger password policies.
- Disabling device functionality (like AirPrint).
- Requiring app installation through Apple’s volume purchase program. For more information, see [How to manage iOS and macOS apps purchased through Apple Business Manager with Microsoft Intune](../apps/vpp-apps-ios.md).
- Enforcing additional data transfer restrictions (like blocking iCloud backup).

The policy settings enforced in level 3 include all the policy settings recommended for level 2. The settings listed below include only those that have been added or changed. These settings may have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations.

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Block App store | Yes ||
| App Store, Doc Viewing, Gaming | Block playback of explicit music, podcast, and iTunes U | Yes ||
| App Store, Doc Viewing, Gaming | Block adding Game Center friends | Yes ||
| App Store, Doc Viewing, Gaming | Block Game Center | Yes ||
| App Store, Doc Viewing, Gaming | Block multiplayer gaming | Yes ||
| App Store, Doc Viewing, Gaming | Block access to network drive in Files app | Yes ||
| Built-in Apps | Block Siri | Yes | |
| Built-in Apps | Block iTunes store | Yes | |
| Built-in Apps | Block Find My Friends | Yes | |
| Built-in Apps | Block user modification to the Find My Friends settings | Yes | |
| Built-in Apps | Block Safari Autofill | Yes | |
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
| General | Block use of erase all content and settings | Yes |  |
| General | Block configuration profile changes | Yes |  |
| General | Block removing apps | Yes |  |
| General | Force automatic data and time | Yes |  |
| General | Block VPN creation | Yes |  |
| General | Block modification of eSIM settings | Yes |  |
| Password | Number of sign-in failures before wiping the device | 5 | Organizations may need to update this setting to match their password policy. |
| Password | Password expiration (days) | 365 | Organizations may need to update this setting to match their password policy. |
| Password | Prevent reuse of previous passwords | 5 | Organizations may need to update this setting to match their password policy. |
| Password | Block password AutoFill | Yes | |
| Wireless | Block voice dialing while device is locked | Yes |  |
| Wireless | Require joining Wi-Fi networks only using configuration profiles | Not configured | Care should be taken when using this setting as this could affect your ability to connect to the device if the specified Wi-Fi Networks are unavailable or if the setting is configured incorrectly. This could result in a situation where you are locked out of the device and unable to remotely reset the device.   |

## Next steps

Administrators can incorporate the above configuration levels within their ring deployment methodology for testing and production use by importing the sample [iOS/iPadOS Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/iOS) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).
