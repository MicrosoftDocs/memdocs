---
# required metadata

title: Android Enterprise security configuration framework
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings suggested for Android Enterprise device basic and high security.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
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

# Android Enterprise work profile security configurations

As part of the [Android Enterprise security configuration framework](android-configuration-framework.md), apply the following settings for Android Enterprise work profile mobile users. For more information on each policy setting, see [Android Enterprise settings to mark devices as compliant or not compliant using Intune](../protect/compliance-policy-create-android-for-work.md#work-profile).

When choosing your settings, be sure to review and categorize usage scenarios. Then, configure users following the guidance for the chosen security level. You can adjust the suggested settings based on the needs of your organization. Make sure to have your security team evaluate the threat environment, risk appetite, and impact to usability.

For personally-owned work profile devices, there are two recommended security configuration frameworks:

- [Work profile basic security (level 1)](#work-profile-basic-security) 
- [Work profile high security (level 3)](#work-profile-high-security) 

> [!Note]
> Because of the settings available for Android Enterprise work profile devices, there is no enhanced security (level 2) offering. The available settings don't justify a difference between level 1 and level 2.

## Work profile basic security

Level 1 is the recommended minimum security configuration for personal devices where users access work or school data. This configuration can apply to most mobile users. Some of the controls may impact user experience.

### Device compliance

| Section | Setting | Value | Notes |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Require the device to be at or under the machine risk score | Not configured ||
| Device Health | Rooted devices | Block ||
| Device Health | Require the device to be at or under the Device Threat Level | Not configured||
| Device Health | Google Play Services is configured | Require ||
| Device Health | Up-to-date security provider | Require ||
| Device Health | Up-to-date security provider | Require ||
| Device Health | SafetyNet device attestation | Check basic integrity & certified devices | This setting configures Google's SafetyNet Attestation on end-user devices. Basic integrity validates the integrity of the device. Rooted devices, emulators, virtual devices, and devices with signs of tampering fail basic integrity.<br>Basic integrity and certified devices validates the compatibility of the device with Google's services. Only unmodified devices that have been certified by Google can pass this check. |
| Device Properties | Minimum OS version | Format: Major.Minor<br>Example: 5.0
| Microsoft recommends configuring the minimum Android major version to match the supported Android versions for Microsoft apps. OEMs and devices adhering to Android Enterprise recommended requirements must support the current shipping release + one letter upgrade. Currently, Android recommends Android 8.0 and later for knowledge workers. For Android's latest recommendations, see [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/). |
| Device Properties | Maximum OS version | Not configured ||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| System Security ||||
| Actions for noncompliance | Mark device noncompliant | Immediately | By default, the policy is configured to mark the device as noncompliant. Additional actions are available. For more information, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance).|



### Device restrictions

## Work profile high security

Level 3 is the recommended configuration for devices used by users or groups who are uniquely high risk. For example, users who handle highly sensitive data where unauthorized disclosure causes considerable material loss. An organization likely to be targeted by well-funded and sophisticated adversaries should aspire to this configuration.


## Next steps

[Android Enterprise fully managed security settings](android-fully-managed-settings.md)