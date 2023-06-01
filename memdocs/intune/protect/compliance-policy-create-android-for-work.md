---
# required metadata

title: Android Enterprise compliance settings in Microsoft Intune
description: See a list of all the settings you can use when setting compliance for your Android Enterprise devices in Microsoft Intune. Set password rules, choose a minimum or maximum operating system version, restrict specific apps, prevent reusing password, and more.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/14/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid: 9da89713-6306-4468-b211-57cfb4b51cc6

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Device compliance settings for Android Enterprise in Intune

This article lists and describes the different compliance settings you can configure on Android Enterprise devices in Intune. As part of your mobile device management (MDM) solution, use these settings to mark rooted devices as not compliant, set an allowed threat level, enable Google Play Protect, and more.

This feature applies to:

- Android Enterprise

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

> [!IMPORTANT]
> To apply to Android Enterprise dedicated devices, compliance policy must target devices, not users. Compliance policies will be evaluated against the device and will appropriately reflect the compliance state in Intune. To allow users on dedicated devices to sign-in to resources protected by Conditional Access policies, consider using Android Enterprise dedicated devices with [*Azure AD shared device mode*](../enrollment/android-kiosk-enroll.md).
>
> On Android Enterprise dedicated devices that are enrolled without Azure AD shared device mode, users of the device will be unable to sign into resources protected by Conditional Access policies, even if the device is compliant in Intune. To learn  more about shared device mode, see [*Overview of shared device mode*](/azure/active-directory/develop/msal-shared-devices) in the Azure AD documentation.

<!-- Compliance policies also apply Android Enterprise dedicated devices. If a compliance policy is assigned to a dedicated device, the device may show as **Not compliant**. Conditional Access and enforcing compliance isn't available on dedicated devices. Be sure to complete any tasks or actions to get dedicated devices compliant with your assigned policies.  -->

## Before you begin

When configuring compliance policies, the broad range of settings enable you to tailor protection to your specific needs. To better understand how to implement specific security configuration scenarios, see the security configuration framework guidance for Android Enterprise device restriction policies.

The security configuration framework is organized into distinct configuration levels that provide guidance for personally owned and supervised devices, with each level building off the previous level. The available levels and settings in each level vary by enrollment mode:

- For Android Enterprise personally-owned work profile devices: [Android personally-owned work profile security settings](../enrollment/android-work-profile-security-settings.md)
- For Android Enterprise fully managed, dedicated, and corporate-owned work profile devices: [Android fully managed-security settings](../enrollment/android-fully-managed-security-settings.md)

When ready to proceed, [create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Android Enterprise**.

## Fully Managed, Dedicated, and Corporate-Owned Work Profile

### Microsoft Defender for Endpoint

- **Require the device to be at or under the machine risk score**  

  Select the maximum allowed machine risk score for devices evaluated by Microsoft Defender for Endpoint. Devices that exceed this score get marked as noncompliant.
  - **Not configured** (*default*)
  - **Clear**
  - **Low**
  - **Medium**
  - **High**

> [!NOTE]
> Microsoft Defender for Endpoint may not be supported on all Android Enterprise enrollment types. [Learn more about what scenarios are supported](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android#installation-instructions).

### Device Health

- **Require the device to be at or under the Device Threat Level**  
  Select the maximum allowed device threat level evaluated by your [mobile threat defense service](mobile-threat-defense.md). Devices that exceed this threat level are marked noncompliant. To use this setting, choose the allowed threat level:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Secured** - This option is the most secure, and means that the device can't have any threats. If the device is detected with any level of threats, it's evaluated as noncompliant.
  - **Low**: - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium** - The device is evaluated as compliant if the threats that are present on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High** - This option is the least secure, as it allows all threat levels. It may be useful if you're using this solution only for reporting purposes.
  
> [!NOTE]
> All the Mobile Threat Defense (MTD) providers are supported on Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile deployments using app configuration. Check with your MTD provider for the exact configuration needed to support Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile platforms on Intune.

#### Google Play Protect

> [!IMPORTANT]
> Devices operating in regions or countries where Google Mobile Services are not available will fail Google Play Protect compliance policy setting evaluations. For more information, see [Managing Android devices where Google Mobile Services are not available](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-customer-success-managing-android-devices-where-google/ba-p/1628793).

- **Google's device integrity check**  
  Enter the level of Google's [Play Integrity](https://developer.android.com/google/play/integrity) that must be met. Your options:

  - **Not configured** (*default*) - Setting isn't evaluated for compliance or non-compliance.
  - **Check basic integrity**
  - **Check basic integrity & certified devices**

### Device Properties

#### Operating System Version

- **Minimum OS version**  
  When a device doesn't meet the minimum OS version requirement, it's reported as non-compliant. A link with information on how to upgrade is shown. The end user can upgrade their device, and then access organization resources.

  *By default, no version is configured*.

- **Maximum OS version**  
  When a device is using an OS version later than the version in the rule, access to organization resources is blocked. The user is asked to contact their IT administrator. Until a rule is changed to allow the OS version, this device can't access organization resources.

  *By default, no version is configured*.

- **Minimum security patch level**  
  Select the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the YYYY-MM-DD format.

  *By default, no date is configured*.

### System Security

- **Require a password to unlock mobile devices**  
  - **Not configured** (*default*) -  This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Users must enter a password before they can access their device.

- **Required password type**  
  Choose if a password should include only numeric characters, or a mix of numerals and other characters. Your options:
  - **Device default** - To evaluate password compliance, be sure to select a password strength other than *Device default*.
  - **Password required, no restrictions**
  - **Weak biometric** - [Strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android's web site)
  - **Numeric** (*default*): Password must only be numbers, such as `123456789`. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **Numeric complex** - Repeated or consecutive numbers, such as "1111" or "1234", aren't allowed. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **Alphabetic** - Letters in the alphabet are required. Numbers and symbols aren't required. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **Alphanumeric** - Includes uppercase letters, lowercase letters, and numeric characters. Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **Alphanumeric with symbols** - Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.

  Depending on the *password type* you select, the following settings are available:
  - **Minimum password length**  
    Enter the minimum length the password must have, between 4 and 16 characters.  

  - **Number of characters required**  
    Enter the number of characters the password must have, between 0 and 16 characters.

  - **Number of lowercase characters required**  
    Enter the number of lowercase characters the password must have, between 0 and 16 characters.

  - **Number of uppercase characters required**  
    Enter the number of uppercase characters the password must have, between 0 and 16 characters.

  - **Number of non-letter characters required**  
    Enter the number of non-letters (anything other than letters in the alphabet) the password must have, between 0 and 16 characters.

  - **Number of numeric characters required**  
    Enter the number of numeric characters (`1`, `2`, `3`, and so on) the password must have, between 0 and 16 characters.

  - **Number of symbol characters required**  
    Enter the number of symbol characters (`&`, `#`, `%`, and so on) the password must have, between 0 and 16 characters.

  - **Maximum minutes of inactivity before password is required**  
    Enter the idle time before the user must reenter their password. Options include the default of *Not configured*, and from *1 Minute* to *8 hours*.

  - **Number of days until password expires**  
    Enter the number of days, between 1-365, until the device password must be changed. For example, to change the password after 60 days, enter `60`. When the password expires, users are prompted to create a new password.

    *By default, no value is configured*.

  - **Number of passwords required before user can reuse a password**  
    Enter the number of recent passwords that can't be reused, between 1-24. Use this setting to restrict the user from creating previously used passwords.  

    *By default, no version is configured*.

#### Encryption

- **Encryption of data storage on device**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Encrypt data storage on your devices.

  You don't have to configure this setting because Android Enterprise devices enforce encryption.

## Personally-Owned Work Profile

### Microsoft Defender for Endpoint - *for Personally-Owned Work Profile*

- **Require the device to be at or under the machine risk score**  
  Select the maximum allowed machine risk score for devices evaluated by Microsoft Defender for Endpoint. Devices that exceed this score get marked as noncompliant.
  - **Not configured** (*default*)
  - **Clear**
  - **Low**
  - **Medium**
  - **High**

### Device Health - *for Personally-Owned Work Profile*

- **Rooted devices**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Mark rooted devices as not compliant.

- **Require the device to be at or under the Device Threat Level**  
  Select the maximum allowed device threat level evaluated by your [mobile threat defense service](mobile-threat-defense.md). Devices that exceed this threat level are marked noncompliant. To use this setting, choose the allowed threat level:
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Secured** - This option is the most secure, and means that the device can't have any threats. If the device is detected with any level of threats, it's evaluated as noncompliant.
  - **Low** - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium** - The device is evaluated as compliant if the threats that are present on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High** - This option is the least secure, as it allows all threat levels. It may be useful if you're using this solution only for reporting purposes.

#### Google Play Protect - *for Personally-Owned Work Profile*

- **Google Play Services is configured**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Require that the Google Play services app is installed and enabled. Google Play services allows security updates, and is a base-level dependency for many security features on certified-Google devices.
  
- **Up-to-date security provider**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Require that an up-to-date security provider can protect a device from known vulnerabilities.
  
- **Google's device integrity check**  
  Enter the level of Google's [Play Integrity](https://developer.android.com/google/play/integrity) that must be met. Your options:
  - **Not configured** (*default*) - Setting isn't evaluated for compliance or non-compliance.
  - **Check basic integrity**
  - **Check basic integrity & certified devices**

- **Required device integrity evaluation type**  
  This setting is only available when *device integrity check* is set to either *Check basic integrity* or *Check basic integrity & certified devices*.

  Select the evaluation type you want to use to compute the Play Integrity device attestation response.

  - **Not configured (defaults to basic evaluation)** – (*default*)
  - **Hardware-backed key** – Require that hardware-backed key attestation is used for Play Integrity evaluation. Devices that don’t support hardware-backed key attestation are marked as not compliant.

  For more information about Play Integrity and which devices support hardware-backed key attestation, see [Play integrity](https://developer.android.com/google/play/integrity) in the Play Integrity documentation for Android.
> [!NOTE]
> On Android Enterprise devices, **Threat scan on apps** is a device configuration policy. Using a configuration policy, administrators can enable the setting on a device. See [Android Enterprise device restriction settings](../configuration/device-restrictions-android-for-work.md).

### Device Properties - *for Personally-Owned Work Profile*

#### Operating System Version - *for Personally-Owned Work Profile*

- **Minimum OS version**  
When a device doesn't meet the minimum OS version requirement, it's reported as non-compliant. A link with information on how to upgrade is shown. The end user can upgrade their device, and then access organization resources.

  *By default, no version is configured*.

- **Maximum OS version**  
When a device is using an OS version later than the version in the rule, access to organization resources is blocked. The user is asked to contact their IT administrator. Until a rule is changed to allow the OS version, this device can't access organization resources.

  *By default, no version is configured*.

### System security - *for Personally-Owned Work Profile*

#### Encryption - *for Personally-Owned Work Profile*

- **Require encryption of data storage on device**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** -  Encrypt data storage on your devices.  

  You don't have to configure this setting because Android Enterprise devices enforce encryption.

#### Device Security - *for Personally-Owned Work Profile*

- **Block apps from unknown sources**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Block devices with **Security** > **Unknown Sources** enabled sources (*supported on Android 4.0 through Android 7.x. Not supported by Android 8.0 and later*).  

  To side-load apps, unknown sources must be allowed. If you're not side-loading Android apps, then set this feature to **Block** to enable this compliance policy.

  > [!IMPORTANT]
  > Side-loading applications require that the **Block apps from unknown sources** setting is enabled. Enforce this compliance policy only if you're not side-loading Android apps on devices.

  You don't have to configure this setting as Android Enterprise devices always restrict installation from unknown sources.

- **Company portal app runtime integrity**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Choose *Require* to confirm the Company Portal app meets all the following requirements:
    - Has the default runtime environment installed
    - Is properly signed
    - Isn't in debug-mode
    - Is installed from a known source

- **Block USB debugging on device**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Prevent devices from using the USB debugging feature.  

  You don't have to configure this setting because USB debugging is already disabled on Android Enterprise devices.

- **Minimum security patch level**  
  Select the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the YYYY-MM-DD format.

  *By default, no date is configured*.

- **Require a password to unlock mobile devices**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Users must enter a password before they can access their device.  

  This setting applies at the device level. If you only need to require a password at the Personally-Owned Work Profile level, then use a configuration policy. See [Android Enterprise device configuration settings](../configuration/device-restrictions-android-for-work.md).

#### All Android devices  - *for Personally-Owned Work Profile*

- **Number of days until password expires**  
  Enter the number of days, between 1-365, until the device password must be changed. For example, to change the password after 60 days, enter `60`. When the password expires, users are prompted to create a new password.

- **Number of previous passwords to prevent reuse**  
  Enter the number of recent passwords that can't be reused. Use this setting to restrict the user from creating previously used passwords.

- **Maximum minutes of inactivity before password is required**  
  Enter the idle time before the user must reenter their password. Options include the default of *Not configured*, and from *1 Minute* to *8 hours*.

#### Android 12 and later - *for Personally-Owned Work Profile*

- **Password complexity**  
  Use this setting to set the password complexity requirements. Your options:

  - **None** - This setting isn't evaluated for compliance or non-compliance.
  - **Low** - A pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are allowed.
  - **Medium** - PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least 4 characters.
  - **High** - PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters.

  On personally owned devices with a work profile, there are two passwords affected by this **Password complexity** setting:

  - The device password that unlocks the device
  - The work profile password that allows users to access the work profile

  If the device password complexity is too low, then the device password is automatically changed to require a **High** complexity. The end users must update the device password to meet the complexity requirements. Then, they sign into the work profile and are prompted to update the work profile complexity configured in the **Password complexity** setting in your policy.

  > [!IMPORTANT]
  >
  > Before the **Password complexity** setting was available, the **Required password type** and **Minimum password length** settings were used. These settings are still available, but they're deprecated by Google for Android 12+ personally owned devices with a work profile. For information on these settings, go to [Android 11 and earlier](#android-11-and-earlier---for-personally-owned-work-profile) (in this article).
  >
  > Here's what you need to know:
  >
  > - If the **Required password type** setting is changed from the **Device default** value in a policy, then:
  >   - Newly enrolled Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity. So if you don't want a **High** password complexity, then create a new policy for Android Enterprise 12+ devices and configure the **Password complexity** setting.
  >   - Existing Android Enterprise 12+ devices will continue to use the **Required password type** setting and the existing value configured.
  >
  >     If you change an existing policy with the **Required password type** setting that's already configured, then Android Enterprise 12+ devices will automatically use the **Password complexity** setting with the **High** complexity.
  >
  >     For Android Enterprise 12+ devices, it's recommended to configure the **Password complexity** setting.
  > 
  > - If the **Required password type** setting isn't changed from the **Device default** value in a policy, then no password policy is automatically applied to newly enrolled Android Enterprise 12+ devices.

#### Android 11 and earlier - *for Personally-Owned Work Profile*

> [!IMPORTANT]
> 
> - Google is deprecating these **Required password type** and **Minimum password length** settings for Android 12+ personally owned devices with a work profile and replacing it with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).
  > - On Android Enterprise 12+ devices, use the **Password complexity** setting.

- **Required password type**  
  Choose if a password should include only numeric characters, or a mix of numerals and other characters. Your options:
  - **Device Default**: Because the Device Default varies by device model, use one of the other values for more control and consistency across all devices.
  - **Low security biometric**
  - **At least numeric** (*default*): Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **Numeric complex**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **At least alphabetic**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **At least alphanumeric**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.
  - **At least alphanumeric with symbols**: Enter the **minimum password length** a user must enter, between 4 and 16 characters.

Depending on the *Required password type* you select, the following setting is available:

- **Minimum password length**  
    Enter the minimum length the password must have, between 4 and 16 characters.

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for Android](compliance-policy-create-android.md) devices.
