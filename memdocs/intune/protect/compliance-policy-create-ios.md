---
# required metadata

title: iOS/iPadOS device compliance settings in Microsoft Intune
description: See a list of all the settings you can use when setting compliance for your iOS/iPadOS devices in Microsoft Intune. Require an email, check jailbroken or rooted devices, set the allowed minimum and maximum operating system, set any password restrictions, including password length and device inactivity, restrict apps, and more.
keywords:
author: brenduns
ms.author: brenduns 
manager: dougeby
ms.date: 10/20/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid: 3cfb8222-d05b-49e3-ae6f-36ce1a16c61d

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

# Device Compliance settings for iOS/iPadOS in Intune

This article lists and describes the different compliance settings you can configure on iOS/iPadOS devices in Intune. As part of your mobile device management (MDM) solution, use these settings to require an email, mark rooted (jailbroken) devices as not compliant, set an allowed threat level, set passwords to expire, and more.

This feature applies to:

- iOS
- iPadOS

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

## Before you begin

When configuring compliance policies, the broad range of settings enable you to tailor protection to your specific needs. To better understand how to implement specific security configuration scenarios, see the security configuration framework guidance for iOS compliance policies.

The security configuration framework is organized into distinct configuration levels that provide guidance for personally owned and supervised devices, with each level building off the previous level.

For details about the settings for each level:

- For personally owned and for supervised devices, see [iOS/iPadOS device compliance security configurations](../enrollment/ios-ipados-device-compliance-security-configurations.md)

When you're ready to proceed, [create an iOS/iPadOS device compliance policy](create-compliance-policy.md#create-the-policy).

## Email

- **Unable to set up email on the device**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - A managed email account is required. If the user already has an email account on the device, the email account must be removed so Intune can set one up correctly. If no email account exists on the device, the user should contact the IT administrator to configure a managed email account.

  The device is considered non-compliant in the following situations:  
  - The email profile is assigned to a different user group than the user group targeted by the compliance policy.
  - The user already set up an email account on the device that matches the Intune email profile deployed to the device. Intune can't overwrite the user-configured profile, and Intune can't manage it. To be compliant,  the end user must remove the existing email settings. Then, Intune can install the managed email profile.  

For details about email profiles, see [configure access to organization email using email profiles with Intune](../configuration/email-settings-configure.md).

## Device Health

- **Jailbroken devices**  
  *Supported for iOS 8.0 and later*

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Mark rooted (jailbroken) devices as not compliant.  

- **Require the device to be at or under the Device Threat Level**  
  *Supported for iOS 8.0 and later*

  Use this setting to take the risk assessment as a condition for compliance. Choose the allowed threat level:
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Secured** - This option is the most secure, and means that the device can't have any threats. If the device is detected with any level of threats, it's evaluated as non-compliant.
  - **Low** - The device is evaluated as compliant if only low-level threats are present. Anything higher puts the device in a non-compliant status.
  - **Medium** - The device is evaluated as compliant if the threats that are present on the device are low or medium level. If the device is detected to have high-level threats, it's determined to be non-compliant.
  - **High** - This option is the least secure, as it allows all threat levels. It may be useful if you're using this solution only for reporting purposes.

## Device Properties

### Operating System Version  

- **Minimum OS version**  
  *Supported for iOS 8.0 and later*

  When a device doesn't meet the minimum OS version requirement, it's reported as non-compliant. A link with information on how to upgrade is shown. The end user can choose to upgrade their device. After that, they can access organization resources.

- **Maximum OS version**  
  *Supported for iOS 8.0 and later*

  When a device uses an OS version later than the version in the rule, access to organization resources is blocked. The end user is asked to contact their IT administrator. The device can't access organization resources until a rule changes to allow the OS version.

- **Minimum OS build version**  
  *Supported for iOS 8.0 and later*

  When Apple publishes security updates, the build number is typically updated, not the OS version. Use this feature to enter a minimum allowed build number on the device.

- **Maximum OS build version**  
  *Supported for iOS 8.0 and later*

  When Apple publishes security updates, the build number is typically updated, not the OS version. Use this feature to enter a maximum allowed build number on the device.

## System Security

### Password

> [!NOTE]
> After a compliance or configuration policy is applied to an iOS/iPadOS device, users are prompted to set a passcode every 15 minutes. Users are continually prompted until a passcode is set. When a passcode is set for the iOS/iPadOS device, the encryption process automatically starts. The device remains encrypted until the passcode is disabled.

- **Require a password to unlock mobile devices**  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.  
  - **Require** - Users must enter a password before they can access their device. iOS/iPadOS devices that use a password are encrypted.

- **Simple passwords**  
  *Supported for iOS 8.0 and later*

  - **Not configured** (*default*) - Users can create simple passwords like **1234** or **1111**.
  - **Block** - Users can't create simple passwords, such as **1234** or **1111**.

- **Minimum password length**  
  *Supported for iOS 8.0 and later*

  Enter the minimum number of digits or characters that the password must have.

- **Required password type**  
  *Supported for iOS 8.0 and later*

  Choose if a password should have only **Numeric** characters, or if there should be a mix of numbers and other characters (**Alphanumeric**).

- **Number of non-alphanumeric characters in password**  
  Enter the minimum number of special characters, such as `&`, `#`, `%`, `!`, and so on, that must be in the password.

  Setting a higher number requires the user to create a password that is more complex.

- **Maximum minutes after screen lock before password is required**  
  *Supported for iOS 8.0 and later*

  Specify how soon after the screen is locked before a user must enter a password to access the device. Options include the default of *Not configured*, *Immediately*, and from *1 Minute* to *4 hours*.

- **Maximum minutes of inactivity until screen locks**  
  Enter the idle time before the device locks its screen. Options include the default of *Not configured*, *Immediately*, and from *1 Minute* to *15 Minutes*.

- **Password expiration (days)**  
  *Supported for iOS 8.0 and later*

  Select the number of days before the password expires, and they must create a new one.

- **Number of previous passwords to prevent reuse**  
  *Supported for iOS 8.0 and later*

  Enter the number of previously used passwords that can't be used.

### Device Security

- **Restricted apps**  
  You can restrict apps by adding their bundle IDs to the policy. If a device has the app installed, the device is marked as non-compliant.

  - **App name** - Enter a user-friendly name to help you identify the bundle ID.
  - **App Bundle ID** - Enter the unique bundle identifier assigned by the app provider. To find the bundle ID, see [Bundle IDs for native iOS and iPadOS apps](https://support.apple.com/guide/mdm/native-ios-and-ipados-app-bundle-ids-mdm90f60c1ce/web) at Support.apple.com, or contact the software vendor of the app.
  
  > [!NOTE]
  > The *Restricted apps* setting applies to un-managed applications that are installed outside of management context.

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for macOS](compliance-policy-create-mac-os.md) devices.
