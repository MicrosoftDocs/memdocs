---
# required metadata

title: iOS/iPadOS device compliance security configurations
titleSuffix: Microsoft Intune
description: Learn the settings suggested for iOS/iPadOS device basic and high security.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 6/01/2021
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

# iOS/iPadOS device compliance security configurations

As part of the [iOS/iPadOS security configuration framework](ios-ipados-configuration-framework.md), apply the following device compliance settings to mobile users using personal and supervised devices. For more information on each policy setting, see [Device Compliance settings for iOS/iPadOS in Intune](../protect/compliance-policy-create-ios.md).

When choosing your settings, be sure to review and categorize usage scenarios. Then, configure users following the guidance for the chosen security level. You can adjust the suggested settings based on the needs of your organization. Make sure to have your security team evaluate the threat environment, risk appetite, and impact to usability.

Administrators can incorporate the below configuration levels within their ring deployment methodology for testing and production use by importing the sample [iOS/iPadOS Security Configuration Framework JSON templates](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/iOS) with [Intune's PowerShell scripts](https://github.com/microsoftgraph/powershell-intune-samples).

> [!Note]
> Due to the limited number of settings available for device compliance, there is no enhanced security (level 2) offering.

## Basic security (Level 1)

Level 1 is the recommended minimum security configuration for iOS/iPadOS devices where users access work or school data. This configuration is applicable to most mobile users accessing work or school data on a device.

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Email | Unable to set up email on the device | Not configured ||
| Device Health | Jailbroken devices | Block |  |
| Device Health | Require the device to be at or under the Device Threat Level | Not configured||
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 13.7| Microsoft recommends configuring the minimum iOS major version to match the supported iOS versions for Microsoft apps. Microsoft apps support a N-1 approach where N is the current iOS major release version. For minor and build version values, Microsoft recommends ensuring devices are up to date with the respective security updates. For Apple's latest recommendations, see [Apple security updates](https://support.apple.com/HT201222).|
| Device Properties | Maximum OS version | Not configured |  |
| Device Properties | Minimum OS build version  | Not configured |  |
| Device Properties | Maximum OS build version  | Not configured |  |
| Microsoft Defender for Endpoint | Require the device to be at or under the Device Threat Level | Not configured |  |
| System Security | Require a password to unlock mobile devices | Require |  |
| System Security | Simple passwords | Block |  |
| System Security | Minimum password length | 6 | Organizations may need to update this setting to match their password policy. |
| System Security | Required password type | Numeric | Organizations may need to update this setting to match their password policy. |
| System Security | Number of non-alphanumeric characters in password | Not configured |  |
| System Security | Maximum minutes after screen lock before password is required | 5 | Organizations may need to update this setting to match their password policy. |
| System Security | Maximum minutes of inactivity until screen locks | 5 | Organizations may need to update this setting to match their password policy. |
| System Security | Password expiration (days) | Not configured |  |
| System Security | Restricted apps | Not configured |  |
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md). |

## High security (Level 3)

Level 3 is the recommended configuration for both:

- Organizations with large and sophisticated security organizations.
- Specific users and groups who will be uniquely targeted by adversaries. Such organizations are typically targeted by well-funded and sophisticated adversaries.

This configuration expands upon Level 1 by:

- Increasing the minimum operating system version.
- Ensuring that the device is compliant by enforcing the most secure Microsoft Defender for Endpoint or mobile threat defense level.
- Enacting stronger password policies.

The policy settings enforced in level 3 include all the policy settings recommended for level 1. The settings listed below include only those that have been added or changed. These settings may have significant impact to users or applications. They enforce a level of security more appropriate for risks facing targeted organizations. 

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Device Health | Require the device to be at or under the Device Threat Level | Secured | This setting requires a mobile threat defense product. For more information, see [Mobile Threat Defense for enrolled devices](../protect/mtd-device-compliance-policy-create.md).<br>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It is not necessary to deploy both.|
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 14.6| Microsoft recommends configuring the minimum iOS major version to match the supported iOS versions for Microsoft apps. Microsoft apps support a N-1 approach where N is the current iOS major release version. For minor and build version values, Microsoft recommends ensuring devices are up to date with the respective security updates. For Apple's latest recommendations, see [Apple security updates](https://support.apple.com/HT201222).|
| Microsoft Defender for Endpoint | Require the device to be at or under the Device Threat Level | Clear | This setting requires Microsoft Defender for Endpoint. For more information, see [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md).<br>Customers should consider implementing Microsoft Defender for Endpoint or a mobile threat defense solution. It is not necessary to deploy both. |
| System Security | Password expiration (days) | 365 |  |
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md). |

## Next steps

Apply [iOS/iPadOS personal device security configurations](ios-ipados-personal-device-security-configurations.md) or [iOS/iPadOS supervised device security configurations](ios-ipados-supervised-device-security-configurations.md).
