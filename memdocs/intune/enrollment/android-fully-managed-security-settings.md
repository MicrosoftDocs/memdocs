---
# required metadata

title: Android Enterprise fully managed security configurations
titleSuffix: Microsoft Intune
description: Learn the suggested settings for Android Enterprise fully managed basic, enhanced, and high security.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/24/2021
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
ms.collection: M365-identity-device-management
---

# Android Enterprise fully managed security configurations

As part of the [Android Enterprise security configuration framework](android-configuration-framework.md), apply the following settings for Android Enterprise fully managed mobile users. For more information on each policy setting, see [Android Enterprise device owner settings to mark devices as compliant or not compliant using Intune](../protect/compliance-policy-create-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile) and [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile).

When choosing your settings, be sure to review and categorize usage scenarios. Then, configure users following the guidance for the chosen security level. You can adjust the suggested settings based on the needs of your organization. Make sure to have your security team evaluate the threat environment, risk appetite, and impact to usability.

For corporate owned fully-managed devices, there are three recommended security configuration frameworks:

- [Fully managed basic security (level 1)](#fully-managed-basic-security) 
- [Fully managed enhanced security (level 2)](#fully-managed-enhanced-security)
- [Fully managed high security (level 3)](#fully-managed-high-security) 

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [Android Enterprise Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

## Fully managed basic security

Level 1 is the recommended minimum security configuration for mobile devices owned by the organization.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users. This is done by enforcing password policies, a minimum operating system version, SafetyNet Device attestation, and disabling certain device functions (like USB file transfers). 

### Device compliance

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Microsoft Defender for Endpoint | Require the device to be at or under the machine risk score | Not configured ||
| Device Health | Require the device to be at or under the Device Threat Level | Not configured||
| Device Health | SafetyNet device attestation | Check basic integrity & certified devices | This setting configures Google's SafetyNet Attestation on end-user devices. Basic integrity validates the integrity of the device. Rooted devices, emulators, virtual devices, and devices with signs of tampering fail basic integrity.<br>Basic integrity and certified devices validates the compatibility of the device with Google's services. Only unmodified devices that have been certified by Google can pass this check. |
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 9.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |
| Device Properties | Maximum OS version | Not configured ||
| Device Properties | Minimum security patch level | Not configured | Android devices can receive monthly security patches, but the release is dependent on OEMs and/or carriers. Organizations should ensure that deployed Android devices do receive security updates before implementing this setting. For the latest patch releases, see [Android Security Bulletins](https://source.android.com/security/bulletin/). |
| System Security | Require a password to unlock mobile devices | Require ||
| System Security | Required password type | Numeric Complex | Organizations may need to update this setting to match their password policy. |
| System Security | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| System Security | Maximum minutes of inactivity before password is required| 5 | Organizations may need to update this setting to match their password policy.|
| System Security | Number of days until password expires| Not configured ||
| System Security |    Number of passwords required before user can reuse a password | Not configured ||
| System Security | Encryption of data storage on device | Require ||
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md).|

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Screen capture | Not Configured ||
| General | Camera | Not Configured ||
| General | Default permission policy | Device Default ||
| General | Date and Time changes | Not Configured ||
| General | Volume changes | Not Configured ||
| General | Factory reset | Block ||
| General | Safe boot | Block ||
| General | Status bar | Not Configured ||
| General | Roaming data services | Not Configured ||
| General | Wi-Fi setting changes | Not Configured ||
| General | Bluetooth configuration | Not Configured ||
| General | Tethering and access to hotspots | Not Configured ||
| General | USB storage | Not Configured ||
| General | USB file transfer | Block ||
| General | External media | Block ||
| General | Beam data using NFC | Not Configured ||
| General | Debugging features | Not Configured ||
| General | Microphone adjustment | Not Configured ||
| General | Factory reset protection emails | Not Configured ||
| General | Network escape hatch | Not Configured ||
| General | System update | Automatic ||
| General | Notification windows | Not Configured ||
| General | Skip first use hints | Not Configured ||
| System security | Threat scan on apps |Require ||
| Device experience | Enrollment profile type | Fully managed ||
| Device experience | Make Microsoft Launcher the default launcher | Not configured | Organizations may choose to implement Microsoft Launcher to ensure a consistent home screen experience on Fully managed devices. For more information, see [How to Setup Microsoft Launcher on Android Enterprise Fully Managed Devices with Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) |
| Password | Disable lock screen | Not Configured ||
| Password | Disabled lock screen features | 0 selected ||
| Password | Required password type | Numeric Complex ||
| Password | Minimum password length | 6 ||
| Password | Number of days until password expires | Not configured ||
| Password | Number of passwords required before user can reuse a password | Not configured ||
| Password | Number of sign-in failures before wiping device | 10 ||
| Power settings | Time to lock screen | 5 ||
| Power settings | Screen on while device plugged in | Not configured ||
| Users and Accounts | Add new users | Not configured ||
| Users and Accounts | User removal | Not configured ||
| Users and Accounts | Account changes (dedicated devices only) | Not configured ||
| Users and Accounts | Personal Google Accounts | Not configured ||
| Users and Accounts | User can configure credentials | Block ||
| Applications | Allow installation from unknown sources | Not configured ||
| Applications | Allow access to all apps in Google Play store | Not configured | By default, users cannot install personal apps from the Google Play Store on fully managed devices. If organizations would like to allow fully managed devices to be utilized for personal use, consider changing this setting. |
| Applications | App auto-updates | Wi-Fi only | Organizations should adjust this setting as necessary as data plan charges may occur if app updates occur over the cellular network. |

## Fully managed enhanced security

Level 2 is the recommended configuration for company owned devices where users access more sensitive information. These devices are a natural target in enterprises today. These settings don't assume a large staff of highly skilled security personnel. Therefore, they should be accessible to most enterprise organizations. This configuration expands upon the configuration in Level 1 by enacting stronger password policies, and disabling user/account capabilities.

The level 2 settings include all the policy settings recommended for level 1. However, the settings listed below include only those settings that have been added or changed. These settings may have a slightly higher impact to users or to applications. They enforce a level of security more appropriate for risks facing users with access to sensitive information on mobile devices.

### Device compliance

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| System Security | Number of days until password expires | 365 | Organizations may need to update this setting to match their password policy. |
| System Security |    Number of passwords required before user can reuse a password | 5 | Organizations may need to update this setting to match their password policy. |

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Factory reset protection emails | Google account email addresses ||
| General | List of email addresses (Google account email addresses option only) | example@gmail.com | Manually update this policy to specify the Google email addresses of device administrators that can unlock the devices after they are wiped. |
| Device password | Number of days until password expires | 365 | Organizations may need to update this setting to match their password policy. |
| Device password | Number of passwords required before user can reuse a password | 5 | Organizations may need to update this setting to match their password policy. |
| Device password | Number of sign-in failures before wiping device | 5 ||
| Users and Accounts | Add new users | Block ||
| Users and Accounts | User removal | Block ||
| Users and Accounts | Personal Google Accounts | Block ||

## Fully managed high security

Level 3 is the recommended configuration for both:
- organizations with large and sophisticated security organizations.
- specific users and groups who will be uniquely targeted by adversaries.
Such organizations are typically targeted by well-funded and sophisticated adversaries. Therefore, they merit the additional constraints and controls listed below.

This configuration expands upon Level 2 by:
- ensuring that the device is compliant by enforcing the most secure Microsoft Defender for Endpoint or mobile threat defense level.
- increasing the minimum operating system version.
- enforcing additional device restrictions (like disabling unredacted notifications on lock screen).
- requiring apps to always be up-to-date. 

The policy settings enforced in level 3 include all the policy settings recommended for level 2. The settings listed below include only those that have been added or changed. These settings may have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations.


### Device compliance

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Microsoft Defender for Endpoint | Require the device to be at or under the machine risk score | Clear | This setting requires Microsoft Defender for Endpoint. For more information, see Enforce compliance for [Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md).<p> Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It is not necessary to deploy both. |
| Device Health | Require the device to be at or under the Device Threat Level | Secured | This setting requires a mobile threat defense product. For more information, see [Mobile Threat Defense for enrolled devices](../protect/mtd-device-compliance-policy-create.md).<p>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It is not necessary to deploy both.|
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 10.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. See Android Enterprise Recommended requirements for Android's latest recommendations |

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Date and Time changes | Block ||
| General | Tethering and access to hotspots | Block ||
| General | Beam data using NFC | Block ||
| Device password | Disabled lock screen features | Trust Agents, Unredacted Notifications ||
| Applications | App auto-updates | Always | Organizations should adjust this setting as necessary as data plan charges may occur if app updates occur over the cellular network. |


## Next steps

Administrators can incorporate the above configuration levels within their ring deployment methodology for testing and production use by importing the sample [Android Enterprise Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).
