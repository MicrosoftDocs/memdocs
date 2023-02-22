---
# required metadata

title: iOS/iPadOS personal device security configurations
titleSuffix: Microsoft Intune
description: Learn the settings suggested for iOS/iPadOS personal device basic and high security.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 6/01/2021
ms.topic: reference
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
ms.collection:
- tier2
- M365-identity-device-management
---

# iOS/iPadOS personal device security configurations

As part of the [iOS/iPadOS security configuration framework](ios-ipados-configuration-framework.md), apply the following device compliance settings to mobile users using personal devices. For more information on each policy setting, see [iOS/iPadOS device settings in Microsoft Intune](../configuration/device-restrictions-ios.md).

When choosing your settings, be sure to review and categorize usage scenarios. Then, configure users following the guidance for the chosen security level. You can adjust the suggested settings based on the needs of your organization. Make sure to have your security team evaluate the threat environment, risk appetite, and impact to usability.

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [iOS/iPadOS Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/iOS) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

## Personal basic security (Level 1)

Level 1 is the recommended minimum security configuration for iOS/iPadOS personal devices where users access work or school data.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users. This is done by enforcing password policies, device lock characteristics, and disabling certain device functions (e.g., untrusted certificates).  

To simplify the table below, only configured settings are listed. Undocumented device restrictions are not configured.

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Treat AirDrop as an unmanaged destination | Yes ||
| Built-in Apps | Block Siri while device is locked | Yes ||
| Built-in Apps | Require Safari fraud warnings  | Yes ||
| Cloud and Storage | Force encrypted backup | Yes |  |
| Cloud and Storage | Block managed apps from storing data in iCloud | Yes |  |
| Connected Devices | Force Apple Watch wrist detection | Yes |  |
| General | Block untrusted TLS certificates | Yes |  |
| General | Block trusting new enterprise app authors | Yes |  |
| Locked Screen Experience | Block Notification Center access in lock screen | Yes |  |
| Locked Screen Experience | Block Today view in lock screen | Yes |  |
| Password | Require a password | Yes |  |
| Password | Block simple passwords | Yes |  |
| Password | Required password type | Numeric |  |
| Password | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| Password | Number of sign-in failures before wiping the device | 10 | Organizations may need to update this setting to match their password policy. |
| Password | Maximum minutes after screen lock before password is required | 5 | Organizations may need to update this setting to match their password policy. |
| Password | Maximum minutes of inactivity until screen locks  | 5 | Organizations may need to update this setting to match their password policy. |

## Personal enhanced security (Level 2)

Level 2 is the recommended configuration for personal devices where users access more sensitive information. These devices are a natural target in enterprises today. These settings don't assume a large staff of highly skilled security personnel. Therefore, they should be accessible to most enterprise organizations. This configuration is applicable to most mobile users accessing work or school data on a device.

This configuration expands upon the configuration in Level 1 by enacting data sharing controls.

The level 2 settings include all the policy settings recommended for level 1. However, the settings listed below include only those settings that have been added or changed. These settings may have a slightly higher impact to users or to applications. They enforce a level of security more appropriate for risks facing users with access to sensitive information on mobile devices.

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| App Store, Doc Viewing, Gaming | Block viewing corporate documents in unmanaged apps | Yes ||
| App Store, Doc Viewing, Gaming | Block viewing non-corporate documents in corporate apps | Not configured | Enabling this device restriction blocks Outlook for iOS’s ability to export contacts. This setting is not recommended if using Outlook for iOS. For more information, see [Support Tip: Enabling Outlook iOS Contact Sync with iOS12 MDM Controls](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-enabling-outlook-ios-contact-sync-with-ios12-mdm/ba-p/298453). |
| App Store, Doc Viewing, Gaming | Allow managed apps to write contacts to unmanaged contacts accounts | Yes | This setting is needed to allow Outlook for iOS to export contacts when **Block viewing corporate documents in unmanaged apps** is set to *Yes*. For more information, see [Support Tip: Enabling Outlook iOS Contact Sync with iOS12 MDM Controls](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-enabling-outlook-ios-contact-sync-with-ios12-mdm/ba-p/298453). |
| App Store, Doc Viewing, Gaming | Allow copy/paste to be affected by managed open-in | Not configured | Enabling this setting will block personal accounts within managed Microsoft apps from sharing data to unmanaged apps. |
| Built-in Apps | Block Siri for dictation   | Yes ||
| Built-in Apps | Block Siri for translation   | Yes ||
| Cloud Storage | Block backup of enterprise books | Yes |  |
| Cloud Storage | Block notes and highlights sync for enterprise books | Yes |  |
| General | Block sending diagnostic and usage data to Apple | Yes |  |

## Personal high security (Level 3)

Level 3 is the recommended configuration for both:

- Organizations with large and sophisticated security organizations.
- Specific users and groups who will be uniquely targeted by adversaries. Such organizations are typically targeted by well-funded and sophisticated adversaries.

This configuration expands upon Level 2 by:

- Enacting stronger password policies.
- Disabling device functionality (e.g., screenshots and screen recordings).
- Enforcing additional data transfer restrictions (e.g., blocking Handoff).

The policy settings enforced in level 3 include all the policy settings recommended for level 2. The settings listed below include only those that have been added or changed. These settings may have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations.

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Cloud and Storage | Block Handoff | Yes |  |
| Connected Devices | Require AirPlay outgoing requests pairing password | Yes |  |
| Connected Devices | Block Apple Watch auto unlock | Yes |  |
| General | Block screenshots and screen recording | Yes |  |
| Password | Number of sign-in failures before wiping the device | 5 | Organizations may need to update this setting to match their password policy. |
| Password | Password expiration (days) | 365 | Organizations may need to update this setting to match their password policy. |
| Password | Prevent reuse of previous passwords | 5 | Organizations may need to update this setting to match their password policy. |
| Wireless | Block voice dialing while device is locked | Yes |  |

## Next steps

Administrators can incorporate the above configuration levels within their ring deployment methodology for testing and production use by importing the sample [iOS/iPadOS Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/iOS) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples). 

1. [Configure app configuration policies](ios-ipados-app-configuration-policies.md)
2. [Configure device compliance security policies](ios-ipados-device-compliance-security-configurations.md)
3. 🡺 **Configure device security policies for personal devices** (*You are here*)  
4. [Configure device security policies for supervised devices](ios-ipados-supervised-device-security-configurations.md) 
