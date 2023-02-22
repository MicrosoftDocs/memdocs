---
# required metadata

title: Android Enterprise security configurations for personally-owned work profile
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings suggested for Android Enterprise device basic and high security.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/06/2021
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

# Android Enterprise personally-owned work profile security configurations

As part of the [Android Enterprise security configuration framework](android-configuration-framework.md), apply the following settings for Android Enterprise work profile mobile users. For more information on each policy setting, see [Android Enterprise settings to mark devices as compliant or not compliant using Intune](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile) and [Android Enterprise device settings to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

When choosing your settings, be sure to review and categorize usage scenarios. Then, configure users following the guidance for the chosen security level. You can adjust the suggested settings based on the needs of your organization. Make sure to have your security team evaluate the threat environment, risk appetite, and impact to usability.

For personally-owned work profile devices, there are two recommended security configuration frameworks:

- [Personally-owned work profile enhanced security (level 2)](#personally-owned-work-profile-enhanced-security)
- [Personally-owned work profile high security (level 3)](#personally-owned-work-profile-high-security)

> [!Note]
> Because of the settings available for personally-owned work profile devices, there is no basic security (level 1) offering. The available settings don't justify a difference between level 1 and level 2.

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [Android Enterprise Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

## Personally-owned work profile enhanced security

Level 2 is the recommended minimum security configuration for personal devices where users access work or school data. This configuration can apply to most mobile users. Some of the controls may impact user experience.

### Device compliance

To simplify the table below, only configured settings are listed. Undocumented device compliance settings are not configured.

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Device Health | Rooted devices | Block ||
| Device Health | Google Play Services is configured | Require ||
| Device Health | Up-to-date security provider | Require ||
| Device Health | SafetyNet device attestation | Check basic integrity & certified devices | This setting configures Google's SafetyNet Attestation on end-user devices. Basic integrity validates the integrity of the device. Rooted devices, emulators, virtual devices, and devices with signs of tampering fail basic integrity.<p>Basic integrity and certified devices validates the compatibility of the device with Google's services. Only unmodified devices that have been certified by Google can pass this check. |
| Device Health  | Required SafetyNet evaluation type  | Hardware-backed key  | Hardware backed attestation enhances the existing SafetyNet attestation service check by leveraging a new evaluation type called [Hardware Backed](https://developer.android.com/training/safetynet/attestation#evaluation-types), providing a more robust root detection in response to newer types of rooting tools and methods that cannot always be reliably detected by a software only solution.<p> As its name implies, hardware backed attestation leverages a hardware-based component which shipped with devices installed with Android 8.1 and later. Devices that were upgraded from an older version of Android to Android 8.1 are unlikely to have the hardware-based components necessary for hardware backed attestation. While this setting should be widely supported starting with devices that shipped with Android 8.1, Microsoft strongly recommends testing devices individually before enabling this policy setting broadly.</p>  |
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 9.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |
| System Security | Require a password to unlock mobile devices | Require ||
| System Security | Required password type | Numeric Complex | Organizations may need to update this setting to match their password policy. |
| System Security | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| System Security | Maximum minutes of inactivity before password is required| 5 | Organizations may need to update this setting to match their password policy.|
| System Security | Encryption of data storage on device | Require ||
| System Security | Block apps from unknown sources | Block ||
| System Security | Company Portal app runtime integrity | Require ||
| System Security | Block USB debugging on device | Block | While this setting blocks debugging using a USB device, it also disables the ability to gather logs which may be useful in troubleshooting purposes. |
| System Security | Minimum security patch level | Not configured | Android devices can receive monthly security patches, but the release is dependent on OEMs and/or carriers. Organizations should ensure that deployed Android devices do receive security updates before implementing this setting. For the latest patch releases, see [Android Security Bulletins](https://source.android.com/security/bulletin/). |
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md).|

### Device restrictions

To simplify the table below, only configured settings are listed. Undocumented device restrictions are not configured.

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Work profile settings | Copy and paste between work and personal profiles | Block ||
| Work profile settings | Data sharing between work and personal profiles | Apps in work profile can handle sharing request from personal profile ||
| Work profile settings | Work profile notifications while device locked | Not configured | Blocking this setting ensures sensitive data is not exposed in work profile notifications, which may impact usability. |
| Work profile settings | Default app permissions | Device Default | Admins need to review and adjust the permissions granted by apps they are deploying. |
| Work profile settings | Add and remove accounts | Block ||
| Work profile settings | Contact sharing via Bluetooth | Enable | By default, access to work contacts is not available on other devices, like automobiles via Bluetooth integration. Enabling this setting improves hands free user experiences. However, the Bluetooth device may cache the contacts upon first connection. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Screen capture | Block ||
| Work profile settings | Search work contacts from personal profile | Not configured | Blocking users from accessing work contacts from the personal profile may impact certain usability scenarios like text messaging and dialer experiences within the personal profile. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Allow widgets from work profile apps | Enable ||
| Work profile settings | Require Work Profile Password | Require ||
| Work profile settings | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| Work profile settings | Maximum minutes of inactivity until work profile locks| 5 | Organizations may need to update this setting to match their password policy. |
| Work profile settings | Number of sign-in failures before wiping the work profile| 10 | Organizations may need to update this setting to match their password policy. |
| Work profile settings | Password expiration (days) | Not configured | Organizations may need to update this setting to match their password policy. |
| Work profile settings | Required password type | Numeric complex ||
| Work profile settings | Prevent reuse of previous passwords | Not configured | Organizations may need to update this setting to match their password policy.|
| Device password | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| Device password | Maximum minutes of inactivity until screen locks | 5 | Organizations may need to update this setting to match their password policy. |
| Device password | Number of sign-in failures before wiping device | 10 | This setting triggers a work profile wipe, and not a wipe of the device. |
| Device password | Password expiration (days) | Not configured | Organizations may need to update this setting to match their password policy. |
| Device password | Required password type | Numeric complex ||
| Device password | Prevent reuse of previous passwords | Not configured | Organizations may need to update this setting to match their password policy. |
| System Security | Threat scan on apps | Require | This setting ensures that Google's Verify Apps scan is turned on for end user devices. If configured, the end user will be blocked from access until they turn on Google's app scanning on their Android device. |
| System Security | Prevent app installations from unknown sources in the personal profile | Block ||

> [!Note]
> When a personally-owned work profile is enabled, “One Lock” is configured by default to combine device and work profile passcodes. One Lock may be disabled to separate work profile and device passcodes if necessary, under work profile settings.

## Personally-owned work profile high security

Level 3 is the recommended configuration for devices used by users or groups who are uniquely high risk. For example, users who handle highly sensitive data where unauthorized disclosure causes considerable material loss. An organization likely to be targeted by well-funded and sophisticated adversaries merit the additional constraints described below. This configuration expands upon the configuration in Level 2 by:

- implementing mobile threat defense or Microsoft Defender for Endpoint.
- restricting personally-owned work profile data scenarios.
- enacting stronger password policies.

The policy settings enforced in level 3 include all the policy settings recommended for level 1. However, the settings listed below include only those that have been added or changed. These settings may have a slightly higher impact to users or applications. They enforce a level of security more appropriate for risks facing users with access to sensitive information on mobile devices.

### Device compliance

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Microsoft Defender for Endpoint | Require the device to be at or under the machine risk score | Clear | This setting requires Microsoft Defender for Endpoint. For more information, see Enforce compliance for [Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md).<p>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It is not necessary to deploy both. |
| Device Health | Require the device to be at or under the Device Threat Level | Secured | This setting requires a mobile threat defense product. For more information, see [Mobile Threat Defense for enrolled devices](../protect/mtd-device-compliance-policy-create.md).<p>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It is not necessary to deploy both.|
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 11.0| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 9.0 and later for knowledge workers. See Android Enterprise Recommended requirements for Android's latest recommendations |
| System Security | Number of days until password expires | 365 | Organizations may need to update this setting to match their password policy. |
| System Security | Number of previous passwords to prevent use | 5 | Organizations may need to update this setting to match their password policy. |


### Device restrictions

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Work profile settings | Work profile notifications while device locked | Block | Blocking this setting ensures sensitive data is not exposed in work profile notifications, which may impact usability. |
| Work profile settings | Contact sharing via Bluetooth | Not configured | By default, access to work contacts is not available on other devices, like automobiles via Bluetooth integration. Enabling this setting improves hands free user experiences. However, the Bluetooth device may cache the contacts upon first connection. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Search work contacts from personal profile | Block | Blocking users from accessing work contacts from the personal profile may impact certain usability scenarios like text messaging and dialer experiences within the personal profile. Organizations should consider balancing the usability scenarios with data protection concerns when implementing this setting. |
| Work profile settings | Allow widgets from work profile apps | Not configured ||
| Work profile settings | Number of sign-in failures before wiping the work profile | 5 | Organizations may need to update this setting to match their password policy. |
| Work profile settings | Password expiration (days) | 365 | Organizations may need to update this setting to match their password policy. |
| Work profile settings | Prevent reuse of previous passwords | 5 | Organizations may need to update this setting to match their password policy. |
| Work profile settings | Smart Lock and other trust agents | Block ||
| Device password | Number of sign-in failures before wiping device | 5 | This setting triggers a work profile wipe and not a wipe of the device. |
| Device password | Password expiration (days) | 365 | Organizations may need to update this setting to match their password policy. |
| Device password | Prevent reuse of previous passwords | 5 | Organizations may need to update this setting to match their password policy. |

## Next steps

Administrators can incorporate the above configuration levels within their ring deployment methodology for testing and production use by importing the sample [Android Enterprise Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).
