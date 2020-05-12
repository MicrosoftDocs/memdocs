---
# required metadata

title: Android device compliance settings in Microsoft Intune - Azure | Microsoft Docs
description: See a list of all the settings you can use when setting compliance for your Android devices in Microsoft Intune. Set password rules, choose a minimum or maximum operating system version, restrict specific apps, prevent reusing password, and more.
keywords:
author: brenduns    
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Android settings to mark devices as compliant or not compliant using Intune

This article lists and describes the different compliance settings you can configure on Android devices in Intune. As part of your mobile device management (MDM) solution, use these settings to mark rooted (jailbroken) devices as not compliant, set an allowed threat level, enable Google Play Protect, and more.

This feature applies to:

- Android device administrator

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

## Before you begin

[Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Android device administrator**.

## Device Health

- **Rooted devices**:

  - **Not configured** (*default*) - this setting isn't evaluated for compliance or non-compliance.
  - **Block** - Mark rooted (jailbroken) devices as not compliant.

- **Require the device to be at or under the Device Threat Level**:

  Use this setting to take the risk assessment from a connected Mobile Threat Defense service as a condition for compliance.
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance. 
  - **Secured** - This option is the most secure, as the device can't have any threats. If the device is detected with any level of threats, it's evaluated as noncompliant.
  - **Low** - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium** - The device is evaluated as compliant if existing threats on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High** - This option is the least secure, and allows all threat levels. It may be useful if you're using this solution only for reporting purposes.

### Google Play Protect

- **Google Play Services is configured**:

  Google Play services allows security updates, and is a base-level dependency for many security features on certified-Google devices.

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.  
  - **Require** - Require that the Google Play services app is installed and enabled.  

- **Up-to-date security provider**:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Require that an up-to-date security provider can protect a device from known vulnerabilities.

- **Threat scan on apps**:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Require that the Android **Verify Apps** feature is enabled.

  > [!NOTE]
  > On the legacy Android platform, this feature is a compliance setting. Intune can only check whether this setting is enabled at the device level.

- **SafetyNet device attestation**:

  Enter the level of [SafetyNet attestation](https://developer.android.com/training/safetynet/attestation.html) that must be met. Your options:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Check basic integrity**
  - **Check basic integrity & certified devices**

> [!NOTE]
> To configure Google Play Protect settings using app protection policies, see [Intune app protection policy settings](../apps/app-protection-policy-settings-android.md#conditional-launch) on Android.

## Device Properties

### Operating System Version 

- **Minimum OS version**:

  When a device doesn't meet the minimum OS version requirement, it's reported as noncompliant. A link with information about how to upgrade is shown. The end user can choose to upgrade their device, and then get access to company resources.

  *By default, no version is configured*.

- **Maximum OS version**:

  When a device is using an OS version later than the version specified in the rule, access to company resources is blocked. The user is asked to contact their IT admin. Until a rule is changed to allow the OS version, this device can't access company resources.

  *By default, no version is configured*.

## System Security

### Password

<!-- Removed
- **Minimum password length**: Enter the minimum number of digits or characters that the user's password must have.   


- **Maximum minutes of inactivity before password is required**: Enter the idle time before the user must reenter their password. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

- **Password expiration (days)**: Select the number of days before the password expires and the user must create a new password.

- **Number of previous passwords to prevent reuse**: Enter the number of recent passwords that can't be reused. Use this setting to restrict the user from creating previously used passwords.

-->

- **Require a password to unlock mobile devices**:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Users must enter a password before they can access their device.

- **Required password type**:

  Choose if a password should include only numeric characters, or a mix of numerals and other characters. Your options:

  - **Device Default** - To evaluate password compliance, be sure to select a password strength other than **Device default**.
  - **Low security biometric**
  - **At least numeric**
  - **Numeric complex** - Repeated or consecutive numerals, such as `1111` or `1234`, aren't allowed.
  - **At least alphabetic**
  - **At least alphanumeric**
  - **At least alphanumeric with symbols**

### Encryption

- **Encryption of data storage on a device**:  
  *Supported on Android 4.0 and later, or KNOX 4.0 and later.*

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Encrypt data storage on your devices. Devices are encrypted when you choose the **Require a password to unlock mobile devices** setting.

### Device Security

- **Block apps from unknown sources**:

  - **Not configured** (*default*) - this setting isn't evaluated for compliance or non-compliance.
  - **Block** - Block devices with **Security > Unknown Sources** enabled sources (*supported on Android 4.0 through Android 7.x. Not supported on Android 8.0 and later.*).

  To side-load apps, unknown sources must be allowed. If you're not side-loading Android apps, then set this feature to **Block** to enable this compliance policy.

  > [!IMPORTANT]
  > Side-loading applications require that the **Block apps from unknown sources** setting is enabled. Enforce this compliance policy only if you're not side-loading Android apps on devices.

- **Company portal app runtime integrity**:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Choose *Require* to confirm the Company Portal app meets all the following requirements:

    - Has the default runtime environment installed
    - Is properly signed
    - Isn't in debug-mode
    - Is installed from a known source

- **Block USB debugging on device** *(Android 4.2 or later)*:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Prevent devices from using the USB debugging feature.

- **Minimum security patch level** *(Android 6.0 or later)*:

  Select the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the `YYYY-MM-DD` format.

  *By default, no date is configured*.

- **Restricted apps**:

  Enter the **App name** and **App bundle ID** for apps that should be restricted, and then select **Add**. A device with at least one restricted app installed is marked as non-compliant.

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for Android Enterprise](compliance-policy-create-android-for-work.md) devices.
