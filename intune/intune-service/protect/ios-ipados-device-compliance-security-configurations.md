---
title: iOS/iPadOS device compliance security configurations
description: Review example device compliance configurations of basic, enhanced, and high security for iOS devices.
author: brenduns
ms.author: brenduns
ms.date: 03/20/2025
ms.topic: reference
ms.reviewer:
ms.collection:
- M365-identity-device-management
- highpri
---

# iOS/iPadOS device compliance security configurations examples

In support of the [Microsoft Zero Trust security model](/security/zero-trust/zero-trust-identity-device-access-policies-common), this article provides example configurations you can use with Microsoft Intune to configure iOS/iPad device compliance settings for mobile users using personal and supervised devices. These examples include levels of device security configuration that align with Zero Trust principles.

When using these examples, work with your security team to evaluate the threat environment, risk appetite, and the effect the different levels and configurations can have on usability. After reviewing and adjusting the examples to meet the needs of your organization, you can incorporate them within a ring deployment methodology for testing and production use by importing the sample [iOS/iPadOS Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/iOS) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

> [!Note]
> Due to the limited number of settings available for device compliance, there is no basic security (level 1) offering.

## Enhanced security (level 2)

Level 2 is the recommended minimum security configuration for iOS/iPadOS devices where users access work or school data. This configuration is applicable to most mobile users accessing work or school data on a device.

The following table lists only configured settings. Settings not listed in the table aren't configured in this example.

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Device Health | Jailbroken devices | Block |  |
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 14.8| Microsoft recommends configuring the minimum iOS major version to match the supported iOS versions for Microsoft apps. Microsoft apps support an N-1 approach where N is the current iOS major release version. For minor and build version values, Microsoft recommends ensuring devices are up to date with the respective security updates. For Apple's latest recommendations, see [Apple security updates](https://support.apple.com/HT201222).|
| System Security | Require a password to unlock mobile devices | Require |  |
| System Security | Simple passwords | Block |  |
| System Security | Minimum password length | 6 | Organizations should update this setting to match their password policy. |
| System Security | Required password type | Numeric | Organizations should update this setting to match their password policy. |
| System Security | Maximum minutes after screen lock before password is required | 5 | Organizations should update this setting to match their password policy. |
| System Security | Maximum minutes of inactivity until screen locks | 5 | Organizations should update this setting to match their password policy. |
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md). |

## High security (level 3)

Level 3 is the recommended configuration for both:

- Organizations with large and sophisticated security organizations.
- Specific users and groups who might be uniquely targeted by adversaries.

Such organizations are typically targeted by well-funded and sophisticated adversaries.

This configuration expands upon level 2 by:

- Increasing the minimum operating system version.
- Ensuring that the device is compliant by enforcing the most secure Microsoft Defender for Endpoint or mobile threat defense level.
- Enacting stronger password policies.

The policy settings enforced in level 3 include all the policy settings recommended for level 2. The settings listed in the following table include only those that are added or changed. These settings can have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations.

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Device Health | Require the device to be at or under the Device Threat Level | Secured | This setting requires a mobile threat defense product. For more information, see [Mobile Threat Defense for enrolled devices](../protect/mtd-device-compliance-policy-create.md).<br>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both.|
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 15.0| Microsoft recommends configuring the minimum iOS major version to match the supported iOS versions for Microsoft apps. Microsoft apps support an N-1 approach where N is the current iOS major release version. For minor and build version values, Microsoft recommends ensuring devices are up to date with the respective security updates. For Apple's latest recommendations, see [Apple security updates](https://support.apple.com/HT201222).|
| Microsoft Defender for Endpoint | Require the device to be at or under the machine risk score | Clear | This setting requires Microsoft Defender for Endpoint. For more information, see [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/microsoft-defender-with-intune.md).<br>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It isn't necessary to deploy both. |
| System Security | Password expiration (days) | 365 |  |
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md). |

## Related articles

- [Configure device security policies for personal devices](../protect/ios-ipados-personal-device-security-configurations.md)
- [Configure device security policies for supervised devices](../protect/ios-ipados-supervised-device-security-configurations.md)