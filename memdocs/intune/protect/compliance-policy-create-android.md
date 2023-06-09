---
# required metadata

title: Android device compliance settings in Microsoft Intune
description: View the device compliance settings that are available for  Android device administrator devices in Microsoft Intune.
keywords:
author: brenduns    
ms.author: brenduns
manager: dougeby
ms.date: 09/16/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Device Compliance settings for Android device administrator in Intune

This article lists the compliance settings you can configure on Android device administrator devices in Intune. As part of your mobile device management (MDM) solution, use these settings to mark rooted devices as not compliant, set an allowed threat level, enable Google Play Protect, and more.

This feature applies to:

- Android device administrator

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

## Before you begin

[Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Android device administrator**.

## Microsoft Defender for Endpoint

- **Require the device to be at or under the machine risk score**  

  Select the maximum allowed machine risk score for devices evaluated by Microsoft Defender for Endpoint. Devices that exceed this score get marked as noncompliant.
  - **Not configured** (*default*)
  - **Clear**
  - **Low**
  - **Medium**
  - **High**

## Device Health

- **Devices managed with device administrator**  
  *Device administrator* capabilities are superseded by Android Enterprise.

  - **Not configured** (*default*)
  - **Block** - Blocking device administrator will guide users to move to Android Enterprise Personally-Owned and Corporate-Owned Work Profile management to regain access.

- **Rooted devices**  
  Prevent rooted devices from having corporate access. (This compliance check is supported for Android 4.0 and above.)

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Mark rooted devices as not compliant.

- **Require the device to be at or under the Device Threat Level**  
  Use this setting to take the risk assessment from a connected Mobile Threat Defense service as a condition for compliance.

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Secured** - This option is the most secure, as the device can't have any threats. If the device is detected with any level of threats, it's evaluated as noncompliant.
  - **Low** - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium** - The device is evaluated as compliant if existing threats on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High** - This option is the least secure, and allows all threat levels. It may be useful if you're using this solution only for reporting purposes.

### Google Play Protect

> [!IMPORTANT]
> Devices operating in countries/regions where Google Mobile Services are not available will fail Google Play Protect compliance policy setting evaluations. For more information, see [Managing Android devices where Google Mobile Services are not available](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-customer-success-managing-android-devices-where-google/ba-p/1628793).

- **Google Play Services is configured**  
  Google Play services allows security updates, and is a base-level dependency for many security features on certified-Google devices.

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.  
  - **Require** - Require that the Google Play services app is installed and enabled.  

- **Up-to-date security provider**

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Require that an up-to-date security provider can protect a device from known vulnerabilities.

- **Threat scan on apps**

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Require that the Android **Verify Apps** feature is enabled.

  > [!NOTE]
  > On the legacy Android platform, this feature is a compliance setting. Intune can only check whether this setting is enabled at the device level.

- **Google Play’s device integrity check**  
  Enter the level of Google's [Play Integrity](https://developer.android.com/google/play/integrity) that must be met. Your options:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Check basic integrity**
  - **Check basic integrity & certified devices**

> [!NOTE]
> To configure Google Play Protect settings using app protection policies, see [Intune app protection policy settings](../apps/app-protection-policy-settings-android.md#conditional-launch) on Android.

## Device Properties

### Operating System Version

- **Minimum OS version**  
  When a device doesn't meet the minimum OS version requirement, it's reported as noncompliant. A link with information about how to upgrade is shown. The end user can choose to upgrade their device, and then get access to company resources.

  *By default, no version is configured*.

- **Maximum OS version**  
  When a device is using an OS version later than the version specified in the rule, access to company resources is blocked. The user is asked to contact their IT admin. Until a rule is changed to allow the OS version, this device can't access company resources.

  *By default, no version is configured*.

## System Security

### Encryption

- **Encryption of data storage on a device**  
  *Supported on Android 4.0 and later, or KNOX 4.0 and later.*

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Encrypt data storage on your devices. Devices are encrypted when you choose the **Require a password to unlock mobile devices** setting.

### Device Security

- **Block apps from unknown sources**  
  *Supported on Android 4.0 to Android 7.x. Not supported by Android 8.0 and later*

  - **Not configured** (*default*) - this setting isn't evaluated for compliance or non-compliance.
  - **Block** - Block devices with **Security > Unknown Sources** enabled sources (*supported on Android 4.0 through Android 7.x. Not supported on Android 8.0 and later.*).

  To side-load apps, unknown sources must be allowed. If you're not side-loading Android apps, then set this feature to **Block** to enable this compliance policy.

  > [!IMPORTANT]
  > Side-loading applications require that the **Block apps from unknown sources** setting is enabled. Enforce this compliance policy only if you're not side-loading Android apps on devices.

- **Company portal app runtime integrity**
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Choose *Require* to confirm the Company Portal app meets all the following requirements:

    - Has the default runtime environment installed
    - Is properly signed
    - Isn't in debug-mode

- **Block USB debugging on device**  
  *(Supported on Android 4.2 or later)*

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Prevent devices from using the USB debugging feature.

- **Minimum security patch level**  
  *(Supported on Android 8.0 or later)*

  Select the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the `YYYY-MM-DD` format.

  *By default, no date is configured*.

- **Restricted apps**  
  Enter the **App name** and **App bundle ID** for apps that should be restricted, and then select **Add**. A device with at least one restricted app installed is marked as non-compliant.

### Password

The available settings for passwords vary by the version of Android on the device.

#### All Android devices

*The following settings are supported on Android 4.0 or later, and Knox 4.0 and later.*

- **Maximum minutes of inactivity before password is required**  
  This setting specifies the length of time without user input after which the mobile device screen is locked. Options range from *1 Minute* to *8 Hours*. The recommended value is *15 Minutes*.

  - **Not configured** *(default)*

#### Android 10 and later

*The following settings are supported on Android 10 or later, but not on Knox.*

- **Password complexity**  
 *This setting is supported on Android 10 or later, but not on Samsung Knox. On devices that run Android 9 and earlier or Samsung Knox, settings for the password length and type override this setting for complexity*.

  Specify the required password complexity.

  - **None** *(default)* - No password required.
  - **Low** - The password satisfies one of the following conditions:
    - Pattern
    - Numeric PIN has a repeating (4444) or ordered (1234, 4321, 2468) sequence.
  - **Medium** - The password satisfies one of the following conditions:
    - Numeric PIN doesn’t have a repeating (4444) or ordered (1234, 4321, 2468) sequence, and has minimum length of 4.
    - Alphabetic, with a minimum length of 4.
    - Alphanumeric, with a minimum length of 4.
  - **High** - The password satisfies one of the following conditions:
    - Numeric PIN doesn’t have a repeating (4444) or ordered (1234, 4321, 2468) sequence, and has minimum length of 8.
    - Alphabetic, with a minimum length of 6.
    - Alphanumeric, with a minimum length of 6.

#### Android 9 and earlier or Samsung Knox

*The following settings are supported on Android 9.0 and earlier, and any version of Samsung Knox.*

- **Require a password to unlock mobile devices**  
  This setting specifies whether to require users to enter a password before access is granted to information on their mobile devices. Recommended value: Require  

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Users must enter a password before they can access their device.
  
  When set to *Require*, the following setting can be configured:

  **Required password type**  
  Choose if a password should include only numeric characters, or a mix of numerals and other characters.

  - **Device Default** - To evaluate password compliance, be sure to select a password strength other than **Device default**.
  - **Low security biometric**
  - **At least numeric**
  - **Numeric complex** - Repeated or consecutive numerals, such as `1111` or `1234`, aren't allowed.
  - **At least alphabetic**
  - **At least alphanumeric**
  - **At least alphanumeric with symbols**

  Based on the configuration of this setting, one or more of the following options are available:

  - **Minimum password length**  
    Enter the minimum number of digits or characters that the user's password must have.

  - **Maximum minutes of inactivity before password is required**  
    Enter the idle time before the user must reenter their password. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.

  - **Number of days until password expires**  
    Select the number of days before the password expires and the user must create a new password.

  - **Number of previous passwords to prevent reuse**  
    Enter the number of recent passwords that can't be reused. Use this setting to restrict the user from creating previously used passwords.


## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for Android Enterprise](compliance-policy-create-android-for-work.md) devices.
