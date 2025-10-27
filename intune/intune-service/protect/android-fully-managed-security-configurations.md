---
title: Android Enterprise security configurations for corporate-owned fully managed profiles
description: Review example configurations of basic, enhanced, and high security for devices with Android Enterprise corporate-owned fully managed profiles.
author: brenduns
ms.author: brenduns
ms.date: 03/26/2025
ms.topic: reference
ms.reviewer:
ms.collection:
- M365-identity-device-management
- highpri
---

# Android Enterprise fully managed device security configuration examples

In support of the [Microsoft Zero Trust security model](/security/zero-trust/zero-trust-identity-device-access-policies-common), this article provides example configurations to use with Microsoft Intune to configure both device compliance policy and device restriction policy for Android Enterprise fully managed mobile users. These examples include levels of device security configuration that align with Zero Trust principles.

When using these examples, work with your security team to evaluate the threat environment, risk appetite, and the effect the different levels and configurations can have on usability. After reviewing and adjusting the examples to meet the needs of your organization, implement a ring deployment approach for initial testing followed by production use.

For more information on each policy setting, see:

- [Android Enterprise settings to mark devices as compliant or not compliant using Intune](../protect/compliance-policy-create-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile)
- [Android Enterprise device settings to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-for-work.md)

## Fully managed basic security (level 1)

Level 1 is the recommended minimum security configuration for mobile devices owned by the organization.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users by:

- Enforcing password policies
- Requiring a minimum OS system version
- Disabling certain device functions (like USB file transfers)

Tables in the following sections list only the settings that are included in these examples. Settings not listed in the tables aren't configured.

### Device compliance (level 1)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Device Health | Play Integrity Verdict | Check basic integrity | This setting requires devices to pass Google's Play Integrity API's basic integrity check. It verifies that the device is in a reasonably secure state, which means it isn't rooted or running a custom ROM. |
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 9.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. <br><br> For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |
| Device Properties | Minimum security patch level | Not configured | Android devices can receive monthly security patches, but the release is dependent on OEMs and/or carriers. Organizations should ensure that deployed Android devices do receive security updates before implementing this setting. For the latest patch releases, see [Android Security Bulletins](https://source.android.com/security/bulletin/). |
| System Security | Require a password to unlock mobile devices | Require |  |
| System Security | Required password type | Numeric Complex | Organizations might need to update this setting to match their password policy. |
| System Security | Minimum password length | 6 | Organizations might need to update this setting to match their password policy. |
| System Security | Maximum minutes of inactivity before password is required | 5 | Organizations might need to update this setting to match their password policy.|
| System Security | Require encryption of data storage on device | Require |  |
| System Security | Intune app runtime integrity | Require |  |
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md). |

### Device restrictions (level 1)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Default permission policy (work profile-level) | Device Default |  |
| General | USB file transfer | Block |  |
| General | External media | Block |  |
| General | Factory reset | Block |  |
| General | Data sharing between work and personal profiles | Device Default |  |
| System security | Threat scan on apps |Require |  |
| Device experience | Enrollment profile type | Fully managed |  |
| Device experience | Device experience type | Not configured | Organizations can choose to implement Microsoft Launcher to ensure a consistent home screen experience on Fully managed devices. For more information, see [How to Setup Microsoft Launcher on Android Enterprise Fully Managed Devices with Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134). |
| Device password | Required password type | Numeric complex |  |
| Device password | Minimum password length | 6 |  |
| Device password | Number of sign-in failures before wiping device | 10 |  |
| Power settings | Time to lock screen (work profile-level) | 5 Minutes |  |
| Users and Accounts | User can configure credentials (work profile-level) | Block |  |
| Applications | App auto-updates (work profile-level) | Wi-Fi only | Organizations should adjust this setting as necessary as data plan charges might occur if app updates occur over the cellular network. |
| Applications | Allow access to all apps in Google Play store | Not configured | By default, users can't install personal apps from the Google Play Store on fully managed devices. If organizations would like to allow fully managed devices to be utilized for personal use, consider changing this setting. |
| Work profile password | Required password type | Numeric complex | Organizations might need to update this setting to match their password policy. |
| Work profile password | Minimum password length | 6 | Organizations might need to update this setting to match their password policy. |
| Work profile password | Number of sign-in failures before wiping device | 10 | Organizations might need to update this setting to match their password policy. |

## Fully managed enhanced security (level 2)

Level 2 is the recommended configuration for company owned devices where users access more sensitive information. These devices are a natural target in enterprises today. These settings don't assume a large staff of highly skilled security personnel. Therefore, they should be accessible to most enterprise organizations. This configuration expands upon the configuration in Level 1 by enacting stronger password policies, and disabling user/account capabilities.

The level 2 settings include all the policy settings recommended for level 1. However, the settings listed in the following sections include only those settings that are added or changed. These settings can have a slightly higher impact to users or to applications. They enforce a level of security more appropriate for risks facing users with access to sensitive information on mobile devices.

### Device compliance (level 2)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| System Security | Number of days until password expires | 365 | Organizations might need to update this setting to match their password policy. |
| System Security |    Number of passwords required before user can reuse a password | 5 | Organizations might need to update this setting to match their password policy. |
| Device Health | Play Integrity Verdict | Check basic integrity & device integrity | Require devices to pass Play's basic integrity check and device integrity check. |
| Device Health | Check strong integrity using hardware-backed security features | Check strong integrity | Require devices to pass Play's strong integrity check. Not all devices support this type of check. Intune marks such devices as noncompliant. |

### Device restrictions (level 2)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Factory reset protection emails | Google account email addresses |  |
| General | List of email addresses (Google account email addresses option only) | example@gmail.com | Manually update this policy to specify the Google email addresses of device administrators that can unlock the devices after they're wiped. |
| Device password | Number of days until password expires | 365 | Organizations might need to update this setting to match their password policy. |
| Device password | Number of passwords required before user can reuse a password | 5 | Organizations might need to update this setting to match their password policy. |
| Device password | Number of sign-in failures before wiping device | 5 |  |
| Users and Accounts | Add new users | Block |  |
| Users and Accounts | User removal | Block |  |
| Users and Accounts | Personal Google Accounts | Block |  |
| Work profile password | Number of passwords required before user can reuse a password | 5 | Organizations might need to update this setting to match their password policy. |

## Fully managed high security (level 3)


Level 3 is the recommended configuration for both:

- Organizations with large and sophisticated security organizations.
- Specific users and groups who are uniquely targeted by adversaries.

Such organizations are typically targeted by well-funded and sophisticated adversaries.

This configuration expands upon Level 2 by:

- Ensuring a device is compliant by enforcing the most secure Microsoft Defender for Endpoint or mobile threat defense level.
- Increasing the minimum operating system version.
- Enforcing additional device restrictions (like disabling unredacted notifications on lock screen).
- Requiring apps to always be up-to-date.

The level 3 settings include all the policy settings recommended for level 2. However, the settings listed in the following sections include only those settings that are added or changed. These settings can have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations.

### Device compliance (level 3)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Microsoft Defender for Endpoint | Require the device to be at or under the machine risk score | Clear | This setting requires Microsoft Defender for Endpoint. For more information, see Enforce compliance for [Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/microsoft-defender-with-intune.md).<p> Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both. |
| Device Health | Require the device to be at or under the Device Threat Level | Secured | This setting requires a mobile threat defense product. For more information, see [Mobile Threat Defense for enrolled devices](../protect/mtd-device-compliance-policy-create.md).<p>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both.|
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 11.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. <br><br> For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |

### Device restrictions (level 3)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| General | Date and Time changes | Block |  |
| General | Tethering and access to hotspots | Block |  |
| General | Beam data using NFC (work profile-level) | Block |  |
| General | Search work contacts and display work contact caller-ID in personal profile | Block |  |
| Device password | Disabled lock screen features | - Unredacted notifications <br><br> - Trust Agents (work profile-level) |  |
| Applications | App auto-updates (work profile-level) | Always | Organizations should adjust this setting as necessary as data plan charges might occur if app updates occur over the cellular network. |
| Work profile password | Number of sign-in failures before wiping device | 5 | Organizations might need to update this setting to match their password policy. |

## Related articles

[Configure security settings for personally-owned devices](android-personally-owned-security-configurations.md)
