---
title: Android Enterprise security configurations for personally-owned work profiles
description: Review example configurations of basic, enhanced, and high security for devices with Android Enterprise personally-owned work profiles.
author: brenduns
ms.author: brenduns
ms.date: 03/26/2025
ms.topic: reference
ms.reviewer:
ms.collection:
- M365-identity-device-management
- highpri
---

# Android Enterprise personally-owned work profile security configuration examples

In support of the [Microsoft Zero Trust security model](/security/zero-trust/zero-trust-identity-device-access-policies-common), this article provides example configurations to use with Microsoft Intune to configure both device compliance policy and device restriction policy for Android Enterprise personally-owned mobile users. These examples include levels of device security configuration that align with Zero Trust principles.

When using these examples, work with your security team to evaluate the threat environment, risk appetite, and the effect the different levels and configurations can have on usability. After reviewing and adjusting the examples to meet the needs of your organization, implement a ring deployment approach for initial testing followed by production use.

For more information on each policy setting, see:

- [Android Enterprise settings to mark devices as compliant or not compliant using Intune](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)
- [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md) > Personally owned

> [!NOTE]
> Because of the settings available for personally-owned work profile devices, there's no basic security (level 1) offering. The available settings don't justify a difference between level 1 and level 2.

Tables in the following sections list only the settings that are included in these examples. Settings not listed in the tables aren't configured.

## Personally-owned work profile enhanced security (level 2)

Level 2 is the recommended minimum security configuration for personal devices where users access work or school data. This configuration can apply to most mobile users. Some of the controls might impact user experience.

### Device compliance (level 2)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Device Health | Rooted devices | Block |  |
| Device Health | Google Play Services is configured | Require |  |
| Device Health | Up-to-date security provider | Require |  |
| Device Health | Play Integrity Verdict | Check basic integrity & device integrity | Require devices to pass Play's basic integrity check and device integrity check. |
| Device Health  | Check strong integrity using hardware-backed security features | Check strong integrity | Require devices to pass Play's strong integrity check. Not all devices support this type of check. Intune marks such devices as noncompliant. |
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 9.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. <br><br> For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |
| System Security | Require encryption  of data storage on device | Require |  |
| System Security | Block apps from unknown sources | Block |  |
| System Security | Company Portal app runtime integrity | Require |  |
| System Security | Block USB debugging on device | Block | While this setting blocks debugging using a USB device, it also disables the ability to gather logs which can be useful in troubleshooting purposes. |
| System Security | Minimum security patch level | Not configured | Android devices can receive monthly security patches, but the release is dependent on OEMs and/or carriers. Organizations should ensure that deployed Android devices do receive security updates before implementing this setting. For the latest patch releases, see [Android Security Bulletins](https://source.android.com/security/bulletin/). |
| System Security | Require a password to unlock mobile devices | Require |  |
| System Security | Required password type | Numeric Complex | Organizations might need to update this setting to match their password policy. |
| System Security | Minimum password length | 6 | Organizations might need to update this setting to match their password policy. |
| System Security | Maximum minutes of inactivity before password is required| 5 | Organizations might need to update this setting to match their password policy.|
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md).|

### Device restrictions (level 2)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Work profile settings | Copy and paste between work and personal profiles | Block |  |
| Work profile settings | Data sharing between work and personal profiles | Apps in work profile can handle sharing request from personal profile |  |
| Work profile settings | Work profile notifications while device locked | Not configured | Blocking this setting ensures sensitive data isn't exposed in work profile notifications, which can impact usability. |
| Work profile settings | Default app permissions | Device Default | Admins need to review and adjust the permissions granted by apps they're deploying. |
| Work profile settings | Add and remove accounts | Block |  |
| Work profile settings | Contact sharing via Bluetooth | Enable | By default, access to work contacts isn't available on other devices, like automobiles via Bluetooth integration. Enabling this setting improves hands free user experiences. However, the Bluetooth device might cache the contacts upon first connection. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Screen capture | Block |  |
| Work profile settings | Search work contacts from personal profile | Not configured | Blocking users from accessing work contacts from the personal profile might impact certain usability scenarios like text messaging and dialer experiences within the personal profile. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Allow widgets from work profile apps | Enable |  |
| Work profile settings | Require Work Profile Password | Require |  |
| Work profile settings | Minimum password length | 6 | Organizations might need to update this setting to match their password policy. |
| Work profile settings | Maximum minutes of inactivity until work profile locks| 5 | Organizations might need to update this setting to match their password policy. |
| Work profile settings | Number of sign-in failures before wiping the work profile| 10 | Organizations might need to update this setting to match their password policy. |
| Work profile settings | Password expiration (days) | Not configured | Organizations might need to update this setting to match their password policy. |
| Work profile settings | Required password type | Numeric complex |  |
| Work profile settings | Prevent reuse of previous passwords | Not configured | Organizations might need to update this setting to match their password policy.|
| Device password | Minimum password length | 6 | Organizations might need to update this setting to match their password policy. |
| Device password | Maximum minutes of inactivity until screen locks | 5 | Organizations might need to update this setting to match their password policy. |
| Device password | Number of sign-in failures before wiping device | 10 | This setting triggers a work profile wipe, and not a wipe of the device. |
| Device password | Password expiration (days) | Not configured | Organizations might need to update this setting to match their password policy. |
| Device password | Required password type | Numeric complex |  |
| Device password | Prevent reuse of previous passwords | Not configured | Organizations might need to update this setting to match their password policy. |
| System Security | Threat scan on apps | Require | This setting ensures that Google's Verify Apps scan is turned on for end user devices. If configured, the end user is blocked from access until they turn on Google's app scanning on their Android device. |
| System Security | Prevent app installations from unknown sources in the personal profile | Block |  |

> [!Note]
> When a personally-owned work profile is enabled, "One Lock" is configured by default to combine device and work profile passcodes. One Lock can be disabled to separate work profile and device passcodes if necessary, under work profile settings. For more information, review the setting *One lock for device and work profile* in the [Work Profile Password](../configuration/device-restrictions-android-for-work.md) section of in *Android Enterprise personally owned devices*.

## Personally-owned work profile high security (level 3)

Level 3 is the recommended configuration for devices used by users or groups who are uniquely high risk. For example, users who handle highly sensitive data where unauthorized disclosure causes considerable material loss. An organization likely to be targeted by well-funded and sophisticated adversaries merit additional constraints.

This configuration expands upon the configuration in Level 2 by:

- Implementing mobile threat defense or Microsoft Defender for Endpoint.
- Restricting personally-owned work profile data scenarios.
- Enacting stronger password policies.

The level 3 settings include all the policy settings recommended for level 2. However, the settings listed in the following sections include only those settings that are added or changed. These settings can have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations.

### Device compliance (level 3)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Microsoft Defender for Endpoint | Require the device to be at or under the machine risk score | Clear | This setting requires Microsoft Defender for Endpoint. For more information, see Enforce compliance for [Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md).<p>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both. |
| Device Health | Require the device to be at or under the Device Threat Level | Secured | This setting requires a mobile threat defense product. For more information, see [Mobile Threat Defense for enrolled devices](../protect/mtd-device-compliance-policy-create.md).<p>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both.|
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 11.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. <br><br> For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |
| System Security | Number of days until password expires | 365 | Organizations might need to update this setting to match their password policy. |
| System Security | Number of previous passwords to prevent use | 5 | Organizations might need to update this setting to match their password policy. |

### Device restrictions (level 3)

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Work profile settings | Work profile notifications while device locked | Block | Blocking this setting ensures sensitive data isn't exposed in work profile notifications, which can impact usability. |
| Work profile settings | Contact sharing via Bluetooth | Not configured | By default, access to work contacts isn't available on other devices, like automobiles via Bluetooth integration. Enabling this setting improves hands free user experiences. However, the Bluetooth device might cache the contacts upon first connection. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Search work contacts from personal profile | Block | Blocking users from accessing work contacts from the personal profile might impact certain usability scenarios like text messaging and dialer experiences within the personal profile. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Allow widgets from work profile apps | Not configured |  |
| Work profile settings | Number of sign-in failures before wiping the work profile | 5 | Organizations might need to update this setting to match their password policy. |
| Work profile settings | Password expiration (days) | 365 | Organizations might need to update this setting to match their password policy. |
| Work profile settings | Prevent reuse of previous passwords | 5 | Organizations might need to update this setting to match their password policy. |
| Work profile settings | Smart Lock and other trust agents | Block |  |
| Device password | Number of sign-in failures before wiping device | 5 | This setting triggers a work profile wipe and not a wipe of the device. |
| Device password | Password expiration (days) | 365 | Organizations might need to update this setting to match their password policy. |
| Device password | Prevent reuse of previous passwords | 5 | Organizations might need to update this setting to match their password policy. |

## Related articles

[Configure security settings for fully managed devices](android-fully-managed-security-configurations.md)


