---
# required metadata

title: Android Enterprise compliance settings in Microsoft Intune
description: See a list of all the settings you can use when setting compliance for your Android Enterprise devices in Microsoft Intune. Set password rules, choose a minimum or maximum operating system version, restrict specific apps, prevent reusing password, and more.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/21/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
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
- compliance
- sub-device-compliance
---

# Device compliance settings for Android Enterprise in Intune

This article lists and describes the different compliance settings you can configure on Android Enterprise devices in Intune. As part of your mobile device management (MDM) solution, use these settings to mark rooted devices as noncompliant, set an allowed threat level, enable Google Play Protect, and more.

This feature applies to:

- Android Enterprise

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).  

> [!IMPORTANT]
> It's important to target compliance policies for dedicated devices at groups of devices, not users. Compliance policies will be evaluated against the device and will appropriately reflect the compliance state in Intune. To allow users on dedicated devices to sign in to resources protected by Conditional Access policies, consider using Android Enterprise dedicated devices with [*Microsoft Entra shared device mode*](../enrollment/android-kiosk-enroll.md). In scenarios with fully managed devices, or personal and corporate-owned work profiles, you can target compliance policies at groups of users or devices.  
>
> Users on dedicated devices enrolled without Microsoft Entra shared device mode can't sign into resources protected by Conditional Access policies, even if the device is compliant in Intune. To learn  more about shared device mode, see [*Overview of shared device mode*](/azure/active-directory/develop/msal-shared-devices) in the Microsoft Entra documentation.  

<!-- Compliance policies also apply Android Enterprise dedicated devices. If a compliance policy is assigned to a dedicated device, the device may show as **Not compliant**. Conditional Access and enforcing compliance isn't available on dedicated devices. Be sure to complete any tasks or actions to get dedicated devices compliant with your assigned policies.  -->

## Before you begin  

<!-- Removing section, framework removed for updates. When configuring compliance policies, the broad range of settings enable you to tailor protection to your specific needs. To better understand how to implement specific security configuration scenarios, see the security configuration framework guidance for Android Enterprise device restriction policies.

The security configuration framework is organized into distinct configuration levels that provide guidance for personally owned and supervised devices, with each level building off the previous level. The available levels and settings in each level vary by enrollment mode:

- For Android Enterprise personally-owned work profile devices: [Android personally-owned work profile security settings](../enrollment/android-work-profile-security-settings.md)
- For Android Enterprise fully managed, dedicated, and corporate-owned work profile devices: [Android fully managed-security settings](../enrollment/android-fully-managed-security-settings.md) -->  

[Create a device compliance policy](create-compliance-policy.md#create-the-policy) to access available settings. For **Platform**, select **Android Enterprise**.  


## Fully managed, dedicated, and corporate-owned work profile  
This section describes the compliance profile settings available for fully managed devices, dedicated devices, and corporate-owned devices with work profiles. Setting categories include: 

* Microsoft Defender for Endpoint  
* Device health  
* Device properties  
* System security  

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

### Device health

- **Require the device to be at or under the Device Threat Level**  
  Select the maximum allowed device threat level evaluated by your [mobile threat defense service](mobile-threat-defense.md). Devices that exceed this threat level are marked noncompliant. To use this setting, choose the allowed threat level:

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Secured** - This option is the most secure, and means that the device can't have any threats. If the device is detected with any level of threats, it's evaluated as noncompliant.
  - **Low**: - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium** - The device is evaluated as compliant if the threats that are present on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High** - This option is the least secure, as it allows all threat levels. It may be useful if you're using this solution only for reporting purposes.
  
> [!NOTE]
> All the Mobile Threat Defense (MTD) providers are supported on Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile deployments using app configuration. Check with your MTD provider for the exact configuration needed to support Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile platforms on Intune.

#### Google Play Protect

> [!IMPORTANT]
> Google Play Protect works in locations where Google Mobile Services is available. Devices operating in regions or countries where Google Mobile Services isn't available will fail Google Play Protect compliance policy setting evaluations. For more information, see [Managing Android devices where Google Mobile Services isn't available](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-customer-success-managing-android-devices-where-google/ba-p/1628793).  

- **Play Integrity Verdict**  
    Select the type of integrity checks devices must pass to stay compliant. Intune evaluates Play's integrity verdict to determine compliance. Your options:   

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Check basic integrity**: Require devices to pass Play's basic integrity check.  
  - **Check basic integrity & device integrity**: Require devices to pass Play's basic integrity check and device integrity check.  

- **Check strong integrity using hardware-backed security features**  
  Optionally, you can require devices to pass a *strong integrity check*. This setting is only available if you require basic integrity checks or device integrity checks. Your options:    

  - **Not configured** (*default*)  – This setting isn't evaluated for compliance or noncompliance. Intune assesses the verdict from the basic integrity check by default.  
  - **Check strong integrity** –  Require devices to pass Play's strong integrity check.  Not all devices support this type of check. Intune marks such devices as noncompliant.  

  For more information about Google Play's integrity services, see these Android developer docs:   
  
  - [Google Play's integrity and signing services](https://developer.android.com/google/play/integrity)  
    
  - [Integrity verdicts](https://developer.android.com/google/play/integrity/setup#configure-api)  

### Device properties

#### Operating system version

- **Minimum OS version**  
  When a device doesn't meet the minimum OS version requirement, it's reported as noncompliant. Device users see a link with information about how to upgrade their OS. They can upgrade their device, and then access organization resources.  

  *By default, no version is configured*.

- **Maximum OS version**  
  When a device is using an OS version later than the version in the rule, access to organization resources is blocked. The user is asked to contact their IT administrator. Until a rule is changed to allow the OS version, this device can't access organization resources.

  *By default, no version is configured*.

- **Minimum security patch level**  
  Select the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the YYYY-MM-DD format.

  *By default, no date is configured*.

### System security

- **Require a password to unlock mobile devices**  
  - **Not configured** (*default*) -  This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Users must enter a password before they can access their device.

- **Required password type**  
  Choose if a password should include only numeric characters, or a mix of numerals and other characters. Your options:
  - **Device default** - To evaluate password compliance, be sure to select a password strength other than *Device default*. The OS might not require a device password by default, so it's better to select a different password type for greater control and consistency across all devices.  
  - **Password required, no restrictions**   
  - **Weak biometric** - For more information about this password type, see [strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android Developers Blog).  
  - **Numeric** (*default*) - Password must only be numbers, such as `123456789`. 
  - **Numeric complex** -  Repeated or consecutive numerals, such as `1111` or `1234`, aren't allowed.  
  - **Alphabetic** - Letters in the alphabet are required. Numbers and symbols aren't required.  
  - **Alphanumeric** - Includes uppercase letters, lowercase letters, and numeric characters.  
  - **Alphanumeric with symbols** - Includes uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.

  Other settings vary by password type. The following settings appear when applicable:  
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
    Enter the number of days, between 1 and 365, until the device password must be changed. For example, to require a password change after 60 days, enter `60`. When the password expires, users are prompted to create a new password.  

    *By default, no value is configured*.

  - **Number of passwords required before user can reuse a password**  
    Enter the number of recent passwords that can't be reused, between 1 and 24. Use this setting to restrict the user from creating previously used passwords.  

    *By default, no version is configured*.

#### Encryption

- **Require encryption of data storage on device**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Encrypt data storage on your devices.

  You don't have to configure this setting because Android Enterprise devices enforce encryption.  

#### Device security  

- **Intune app runtime integrity**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Checks that the Intune app has the default runtime environment installed, and is properly signed.  

## Personally owned work profile  
This section describes the compliance profile settings available for personal devices enrolling with work profiles. Setting categories include: 

* Microsoft Defender for Endpoint  
* Device health  
* Device properties  
* System security  

### Microsoft Defender for Endpoint - *for personally owned work profile*

- **Require the device to be at or under the machine risk score**  
  Select the maximum allowed machine risk score for devices evaluated by Microsoft Defender for Endpoint. Devices that exceed this score get marked as noncompliant.
  - **Not configured** (*default*)
  - **Clear**
  - **Low**
  - **Medium**
  - **High**  

### Device health - *for personally owned work profile*

- **Rooted devices**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Block** - Mark rooted devices as not compliant.

- **Require the device to be at or under the Device Threat Level**  
  Select the maximum allowed device threat level evaluated by your [mobile threat defense service](mobile-threat-defense.md). Devices that exceed this threat level are marked noncompliant. To use this setting, choose the allowed threat level:
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Secured** - This option is the most secure, and means that the device can't have any threats. If the device is detected with any level of threats, it's evaluated as noncompliant.
  - **Low** - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium** - The device is evaluated as compliant if the threats that are present on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be noncompliant.
  - **High** - This option is the least secure, as it allows all threat levels. It may be useful if you're using this solution only for reporting purposes.


#### Google Play Protect - *for personally owned work profile*  

> [!IMPORTANT]
> Google Play Protect works in locations where Google Mobile Services is available. Devices operating in regions or countries where Google Mobile Services isn't available will fail Google Play Protect compliance policy setting evaluations. For more information, see [Managing Android devices where Google Mobile Services isn't available](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-customer-success-managing-android-devices-where-google/ba-p/1628793).   

- **Google Play Services is configured**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Require that the Google Play services app is installed and enabled. The Google Play services app enables security updates, and is a base-level dependency for many security features on certified-Google devices.
  
- **Up-to-date security provider**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Require that an up-to-date security provider can protect a device from known vulnerabilities.
  
- **Play Integrity Verdict**  
    Select the type of integrity checks devices must pass to stay compliant. Intune evaluates Play's integrity verdict to determine compliance. Your options:  

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.  
  - **Check basic integrity**: Require devices to pass Play's basic integrity check.  
  - **Check basic integrity & device integrity**: Require devices to pass Play's basic integrity check and device integrity check.  

- **Check strong integrity using hardware-backed security features**  
  Optionally, you can require devices to pass a *strong integrity check*. This setting is only available if you require basic integrity checks or device integrity checks. Your options:   

  - **Not configured** (*default*)  – This setting isn't evaluated for compliance or noncompliance. Intune evaluates the basic integrity check by default.  
  - **Check strong integrity** –  Require devices to pass Play's strong integrity check.  Not all devices support this type of check. Intune marks such devices as noncompliant.  

  For more information about Google Play's integrity services, see these Android developer docs:  
    
  - [Google Play's integrity and signing services](https://developer.android.com/google/play/integrity)
  
  - [Integrity verdicts](https://developer.android.com/google/play/integrity/setup#configure-api)   
  
> [!TIP]
> Intune also has a policy that requires Play Protect to scan installed apps for threats. You can configure this setting in an Android Enterprise device configuration policy under **Device restrictons** > **System security**. For more information, see [Android Enterprise device restriction settings](../configuration/device-restrictions-android-for-work.md).  


### Device properties - *for personally owned work profile*

#### Operating system version - *for personally owned work profile*

- **Minimum OS version**  
When a device doesn't meet the minimum OS version requirement, it's reported as noncompliant. Device users see a link with information about how to upgrade their OS. They can upgrade their device, and then access organization resources.  

  *By default, no version is configured*.  

- **Maximum OS version**  
When a device is using an OS version later than the version in the rule, access to organization resources is blocked. The user is asked to contact their IT administrator. Until a rule is changed to allow the OS version, this device can't access organization resources.

  *By default, no version is configured*.  


### System security - *for personally owned work profile*

#### Encryption - *for personally owned work profile*

- **Require encryption of data storage on device**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.  
  - **Require** -  Encrypt data storage on your devices.  

  You don't have to configure this setting because Android Enterprise devices enforce encryption.  


#### Device security - *for personally owned work profile*

- **Block apps from unknown sources**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Block** - Block devices with **Security** > **Unknown Sources** enabled sources (*supported on Android 4.0 through Android 7.x. Not supported by Android 8.0 and later*).  

  To side-load apps, unknown sources must be allowed. If you're not side-loading Android apps, then set this feature to **Block** to enable this compliance policy.  

  > [!IMPORTANT]
  > Side-loading applications require that the **Block apps from unknown sources** setting is enabled. Enforce this compliance policy only if you're not side-loading Android apps on devices. 

  You don't have to configure this setting as Android Enterprise devices always restrict installation from unknown sources.

- **Company Portal app runtime integrity**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Choose *Require* to confirm the Company Portal app meets all the following requirements:
    - Has the default runtime environment installed
    - Is properly signed
    - Isn't in debug-mode
    - Is installed from a known source

- **Block USB debugging on device**  
- **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
- **Block** - Prevent devices from using the USB debugging feature.  

  You don't have to configure this setting for Android Enterprise fully managed devices, dedicated devices, and corporate-owned devices with work profiles, because USB debugging is already disabled.  
  
- **Minimum security patch level**  
  Select the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the YYYY-MM-DD format.

  *By default, no date is configured*.

- **Require a password to unlock mobile devices**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Users must enter a password before they can access their device.  

  This setting applies at the device level. If you only require a password at the work profile level, use a configuration policy. For more information, see [Android Enterprise device configuration settings](../configuration/device-restrictions-android-for-work.md).  

> [!IMPORTANT]
> When a personally-owned work profile is enabled, the device and work profile passcodes are combined by default so that the same passcode is used in both places. Intune enforces the higher complexity level of the two. The device user can use two separate passcodes if they go to their work profile settings and deselect **Use one lock**. To ensure that device users use two separate passcodes upon enrollment create a device configuration profile that restricts device users from using one lock.  
> 
> 1. In the admin center, create a device configuration profile.   
> 2. For profile type, select **Device restrictions**.  
> 3. Expand **Work profile settings** and go to **Work Profile Password** > **All Android devices**.  
> 4. Find the restriction **One lock for device and work profile**. Select **Block**.  
> 
##### All Android devices  - *device security*  

- **Number of days until password expires**  
  Enter the number of days, between 1-365, until the device password must be changed. For example, to require a password change after 60 days, enter `60`. When the password expires, users are prompted to create a new password.  

- **Number of previous passwords to prevent reuse**  
  Use this setting to restrict users from reusing old passwords. Enter the number of passwords you want to prevent them from reusing, from 1-24. For example, enter `5` so that users can't reuse any of their past 5 passwords. When the value is blank, Intune doesn't change or update this setting. 

- **Maximum minutes of inactivity before password is required**  
  Enter the maximum idle time allowed, from 1 minute to 8 hours. After this amount of time, the user must re-enter their password to get back into their device. When you choose **Not configured** (default), this setting isn't evaluated for compliance or noncompliance.


##### Android 12 and later - *device security*    

- **Password complexity**  
  Select the password complexity requirements for devices running Android 12 and later. Your options:  

  - **None** - This setting isn't evaluated for compliance or noncompliance.
  - **Low** - Patterns or PINs with repeating (4444) or ordered (1234, 4321, 2468) sequences are allowed.
  - **Medium** - The length, alphabetic length, or alphanumeric length must be at least 4 characters. PINs with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.  
  - **High** - The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters. PINs with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.  

  This setting affects two passwords on the device:  

  - The device password that unlocks the device.  
  - The work profile password that allows users to access the work profile.  

  If the device password complexity is too low, then the device password is automatically changed to require a high level of complexity. End users must update the device password to meet the complexity requirements. Then when they sign into the work profile, they are prompted to update their work profile password to match the complexity level you configure under **Work Profile Security** > **Password complexity**.  

  > [!IMPORTANT]
  >
  > Before the password complexity setting was available, the **Required password type** and **Minimum password length** settings were used. These settings are still available, but Google has deprecated them for personal devices with a work profile.       
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


##### Android 11 and earlier - *device security*  

> [!IMPORTANT]
> Google has deprecated the **Required password type** and **Minimum password length** settings for Android 12 and later. In place of those settings, use the password complexity setting under **Android 12 and later**. If you continue to use the deprecated settings without configuring the password complexity setting, new devices running Android 12 or later will default to *high* password complexity. For more information about this change and how it affects passwords on new and existing devices, see [Android 12 and later - device security](#android-12-and-later---device-security) in this article.     

- **Required password type**  
  Choose if a password should include only numeric characters, or a mix of numerals and other characters. Your options:  

  - **Device Default**: To evaluate password compliance, be sure to select a password strength other than *Device default*. The OS might not require a device password by default, so it's better to select a different password type for greater control and consistency across all devices.  
  - **Low security biometric**: For more information about this password type, see [strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android Developers Blog).  
  - **At least numeric** (*default*): Require numeric characters, such as `123456789`.  
  - **Numeric complex**: Repeated or consecutive numerals, such as `1111` or `1234`, aren't allowed. Also enter:  
  - **At least alphabetic**: Require letters from the alphabet. Numbers and symbols aren't required. Also enter:        
  - **At least alphanumeric**: Require uppercase letters, lowercase letters, and numeric characters.      
  - **At least alphanumeric with symbols**: Require uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols. 

- **Minimum password length**  
    This setting appears for certain password types. Enter the minimum number of characters required, between 4 and 16 characters.  

#### Work profile security - *for personally owned work profile*  
If you don't configure password requirements, the use of a work profile password is optional and left up to users to configure.  

- **Require a password to unlock work profile**  
  Require device users to have a password-protected work profile. Your options:  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or noncompliance.
  - **Require** - Users must enter a password to access their work profile.

##### All Android devices - *work profile security*  

- **Number of days until password expires**  
  Enter the number of days, between 1-365, until the work profile password must be changed. For example, to require a password change after 60 days, enter `60`. When the password expires, users are prompted to create a new password.  

- **Number of previous passwords to prevent reuse**  
  Use this setting to restrict users from reusing old passwords. Enter the number of passwords you want to prevent them from reusing, from 1-24. For example, enter *5* so that users can't reuse any of their past 5 passwords. When the value is blank, Intune doesn't change or update this setting.  

- **Maximum minutes of inactivity before password is required**  
  Enter the maximum idle time allowed, from 1 minute to 8 hours. After this amount of time, the user must re-enter their password to get back into their work profile. When you choose **Not configured** (default), this setting isn't evaluated for compliance or noncompliance.  

##### Android 12 and later - *work profile security*  

- **Password complexity**  
  Select the password complexity requirement for work profiles on devices running Android 12 and later. Your options:  

  - **None** - This setting isn't evaluated for compliance or noncompliance.
  - **Low** - A pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are allowed.
  - **Medium** - The length, alphabetic length, or alphanumeric length must be at least 4 characters. PINs with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. 
  - **High** - The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters. PINs with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.  

  This setting affects two passwords on the device:  

  - The device password that unlocks the device.  
  - The work profile password that allows users to access the work profile.    

  If the device password complexity is too low, then the device password is automatically changed to require a high level of complexity. End users must update the device password to meet the complexity requirements. Then when they sign into the work profile, they are prompted to update their work profile password to match the complexity you configure here.  

   > [!IMPORTANT]
  >
  > Before the password complexity setting was available, the **Required password type** and **Minimum password length** settings were used. These settings are still available, but Google has since deprecated them for personal devices with a work profile.     
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

##### Android 11 and earlier - *work profile security*   
These passwords settings apply to devices running Android 11 and earlier.  

> [!IMPORTANT]
> Google has deprecated the **Required password type** and **Minimum password length** settings for Android 12 and later. In place of those settings, use the password complexity setting under **Android 12 and later**. If you continue to use the deprecated settings without configuring the password complexity setting, new devices running Android 12 or later will default to *high* password complexity. For more information about this change and how it affects work profile passwords on new and existing devices, see [Android 12 and later - work profile security](#android-12-and-later---work-profile-security) in this article.    

- **Required password type**  
  Require users to use a certain type of password. Your options:  
  - **Device default** - To evaluate password compliance, be sure to select a password strength other than *Device default*. The OS might not require a work profile password by default, so it's better to select a different password type for greater control and consistency across all devices.  
  - **Low security biometric**: For more information about this password type, see [strong vs. weak biometrics](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (opens Android Developers Blog).  
  - **At least numeric** (*default*): Require numeric characters, such as `123456789`.  
  - **Numeric complex**: Repeated or consecutive numerals, such as `1111` or `1234`, aren't allowed.          
  - **At least alphabetic**: Require letters from the alphabet. Numbers and symbols aren't required.       
  - **At least alphanumeric**: Require uppercase letters, lowercase letters, and numeric characters.  
  - **At least alphanumeric with symbols**: Require uppercase letters, lowercase letters, numeric characters, punctuation marks, and symbols.  
- **Minimum password length**  
    This setting appears for certain password types. Enter the minimum number of characters required, between 4 and 16 characters.  

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for Android](compliance-policy-create-android.md) devices.
