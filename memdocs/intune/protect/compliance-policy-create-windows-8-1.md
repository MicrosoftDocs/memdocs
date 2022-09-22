---
# required metadata

title: Windows 8.1 compliance settings in Microsoft Intune
description: See a list of all the settings you can use when setting compliance for your Windows 8.1 in Microsoft Intune. Check for compliance on the minimum and maximum operating system, set password restrictions and length, enable encryption on data storage, and more.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Device Compliance settings for Windows 8.1 in Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

This article lists and describes the different compliance settings you can configure on Windows 8.1 devices in Intune. As part of your mobile device management (MDM) solution, use these settings to block simple passwords, set a minimum and maximum OS version, and more.

This feature applies to:

- Windows 8.1 and later

As an Intune administrator, use these compliance settings to help protect your organizational resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

## Before you begin

[Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Windows 8.1 and later**.

## Device Properties

### Operating System Version

**Windows 8.1 and later**
- **Minimum OS version**:  
  Enter the minimum allowed version. When a device doesn't meet the minimum OS version requirement, it's reported as non-compliant. A link with information on how to upgrade is shown. The device user can choose to upgrade their device, and then get access to company resources.

- **Maximum OS version**:  
  Enter the maximum allowed version. When a device is using an OS version later than the version entered in the rule, access to organization resources is blocked. The device user is asked to contact their IT administrator. The device can't access organizational resources until a rule changes to allow the OS version.

Windows 8.1 PCs return a version of **3**. If the OS version rule is set to Windows 8.1 for Windows, then the device is reported as non-compliant even if the device has Windows 8.1.

## System Security

### Password

- **Require a password to unlock mobile devices**:  
  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Users must enter a password before they can access their device.

- **Simple passwords**:  
  - **Not configured** (*default*) - Users can create simple passwords like **1234** or **1111**.
  - **Block** - Users can't create simple passwords, such as **1234** or **1111**.  

- **Minimum password length**:  
  Enter the minimum number of digits or characters that the password must have.

  For devices that run Windows and are accessed with a Microsoft account, the compliance policy fails to evaluate correctly if either of the following conditions is met:  
  - Minimum password length is greater than eight characters
  - Minimum number of character sets is more than two

- **Password type**:  
  Choose if a password should have only **Numeric** characters, or if there should be a mix of numbers and other characters (**Alphanumeric**).

  When set to *Alphanumeric*, the following setting is available.  

  - **Number of non-alphanumeric characters in password**:  
    When the *password type* is set to **Alphanumeric**, specify the minimum number of character sets that the password must contain. Options include **0** to **4** sets, with a default of **1**.
    
    The four character sets are:
    - Lowercase letters
    - Uppercase letters
    - Symbols
    - Numbers

    Setting a higher number requires the user to create a password that is more complex. For devices that are accessed with a Microsoft account, the compliance policy fails to evaluate correctly if either of the following conditions is met:

    - Minimum password length is greater than eight characters
    - Minimum number of character sets is more than two

- **Maximum minutes of inactivity before password is required**:  
  Enter the idle time before the user must reenter their password.

- **Password expiration (days)**:  
  Select the number of days before the password expires, and users must create a new one.

- **Number of previous passwords to prevent reuse**:  
  Enter the number of previously used passwords that can't be used.

### Encryption

- **Encryption of data storage on device**:  
  - **Not configured** (*default*)
  - **Require** - Use *Require* to encrypt data storage on your devices.


<!-- not on phone   
- **Require encryption on mobile device**: **Require** the device to be encrypted to connect to data storage resources.
--> 

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- See the [compliance policy settings for Windows 10/11](compliance-policy-create-windows.md) devices.