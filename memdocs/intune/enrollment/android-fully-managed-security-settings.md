---
# required metadata

title: Android Enterprise fully managed security configurations
titleSuffix: Microsoft Intune
description: Learn the suggested settings for Android Enterprise fully managed basic, enhanced, and high security.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/18/2022
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Android Enterprise fully managed security configurations

As part of the [Android Enterprise security configuration framework](android-configuration-framework.md), apply the following settings for Android Enterprise fully managed mobile users. For more information on each policy setting, see [Android Enterprise device owner settings to mark devices as compliant or not compliant using Intune](../protect/compliance-policy-create-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile) and [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile).

When choosing your settings, be sure to review and categorize usage scenarios. Then, configure users following the guidance for the chosen security level. You can adjust the suggested settings based on the needs of your organization. Make sure to have your security team evaluate the threat environment, risk appetite, and impact to usability.

For corporate owned fully managed devices, there are three recommended security configuration frameworks:

- [Fully managed basic security (level 1)](#fully-managed-basic-security) 
- [Fully managed enhanced security (level 2)](#fully-managed-enhanced-security)
- [Fully managed high security (level 3)](#fully-managed-high-security) 

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [Android Enterprise Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

## Fully managed basic security

Level 1 is the recommended minimum security configuration for mobile devices owned by the organization.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users. This is done by enforcing password policies, a minimum operating system version, Google Play's device integrity check, and disabling certain device functions (like USB file transfers).

### Device compliance

To simplify the table below, only configured settings are listed. Undocumented device compliance settings aren't configured.

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Device Health | Google Play's device integrity check | Check basic integrity & certified devices | This setting configures Google Play's device integrity check on end-user devices. Basic integrity validates the integrity of the device. Rooted devices, emulators, virtual devices, and devices with signs of tampering fail basic integrity.<br>Basic integrity and certified devices validates the compatibility of the device with Google's services. Only unmodified devices that have been certified by Google can pass this check. |
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 9.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |
| Device Properties | Minimum security patch level | Not configured | Android devices can receive monthly security patches, but the release is dependent on OEMs and/or carriers. Organizations should ensure that deployed Android devices do receive security updates before implementing this setting. For the latest patch releases, see [Android Security Bulletins](https://source.android.com/security/bulletin/). |
| System Security | Require a password to unlock mobile devices | Require ||
| System Security | Required password type | Numeric Complex | Organizations may need to update this setting to match their password policy. |
| System Security | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| System Security | Maximum minutes of inactivity before password is required| 5 | Organizations may need to update this setting to match their password policy.|
| System Security | Encryption of data storage on device | Require ||
| System Security | Intune app runtime integrity | Require ||
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md).|

### Device restrictions

To simplify the table below, only configured settings are listed. Undocumented device restrictions aren't configured.

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Default permission policy | Device Default ||
| General | Factory reset | Block ||
| General | USB file transfer | Block ||
| General | External media | Block ||
| General | Data sharing between work and personal profiles | Device Default ||
| System security | Threat scan on apps |Require ||
| Device experience | Enrollment profile type | Fully managed ||
| Device experience | Make Microsoft Launcher the default launcher | Not configured | Organizations may choose to implement Microsoft Launcher to ensure a consistent home screen experience on Fully managed devices. For more information, see [How to Setup Microsoft Launcher on Android Enterprise Fully Managed Devices with Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) |
| Device password | Required password type | Numeric Complex ||
| Device password | Minimum password length | 6 ||
| Device password | Number of sign-in failures before wiping device | 10 ||
| Power settings | Time to lock screen | 5 ||
| Users and Accounts | User can configure credentials | Block ||
| Applications | Allow access to all apps in Google Play store | Not configured | By default, users cannot install personal apps from the Google Play Store on fully managed devices. If organizations would like to allow fully managed devices to be utilized for personal use, consider changing this setting. |
| Applications | App auto-updates | Wi-Fi only | Organizations should adjust this setting as necessary as data plan charges may occur if app updates occur over the cellular network. |
| Work profile password | Required password type | Numeric Complex | Organizations may need to update this setting to match their password policy. |
| Work profile password | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| Work profile password | Number of sign-in failures before wiping device | 10 | Organizations may need to update this setting to match their password policy. |

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
| General | List of email addresses (Google account email addresses option only) | example@gmail.com | Manually update this policy to specify the Google email addresses of device administrators that can unlock the devices after they're wiped. |
| Device password | Number of days until password expires | 365 | Organizations may need to update this setting to match their password policy. |
| Device password | Number of passwords required before user can reuse a password | 5 | Organizations may need to update this setting to match their password policy. |
| Device password | Number of sign-in failures before wiping device | 5 ||
| Users and Accounts | Add new users | Block ||
| Users and Accounts | User removal | Block ||
| Users and Accounts | Personal Google Accounts | Block ||
| Work profile password | Number of passwords required before user can reuse a password | 5 | Organizations may need to update this setting to match their password policy. |

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
| Microsoft Defender for Endpoint | Require the device to be at or under the machine risk score | Clear | This setting requires Microsoft Defender for Endpoint. For more information, see Enforce compliance for [Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md).<p> Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both. |
| Device Health | Require the device to be at or under the Device Threat Level | Secured | This setting requires a mobile threat defense product. For more information, see [Mobile Threat Defense for enrolled devices](../protect/mtd-device-compliance-policy-create.md).<p>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both.|
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 11.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. See Android Enterprise Recommended requirements for Android's latest recommendations |

### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Date and Time changes | Block ||
| General | Tethering and access to hotspots | Block ||
| General | Beam data using NFC | Block ||
| General | Search work contacts and display work contact caller-id in personal profile | Block ||
| Device password | Disabled lock screen features | Trust Agents, Unredacted Notifications ||
| Applications | App auto-updates | Always | Organizations should adjust this setting as necessary as data plan charges may occur if app updates occur over the cellular network. |
| Work profile password | Number of sign-in failures before wiping device | 5 | Organizations may need to update this setting to match their password policy. |

## Next steps

Administrators can incorporate the above configuration levels within their ring deployment methodology for testing and production use by importing the sample [Android Enterprise Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).  

1. [Configure device enrollment restrictions for personal devices](device-enrollment-restrictions.md)
2. [Configure app configuration policies](android-app-configuration-policies.md)
3. [Configure security settings for personal devices](android-work-profile-security-settings.md)  
4. 🡺 **Configure security settings for fully managed devices** (*You're here*)  
