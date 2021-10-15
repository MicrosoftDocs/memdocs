---
# required metadata

title: Android AOSP compliance settings in Microsoft Intune
description: View the device compliance settings that are available for AOSP devices in Microsoft Intune.
keywords:
author: brenduns    
ms.author: brenduns
manager: dougeby
ms.date: 10/19/2021
ms.topic: conceptual
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

# Device Compliance settings for Android AOSP in Intune

*This feature is in public preview.*

This article lists the compliance settings you can configure on Android Open Source Project (AOSP) devices in Intune. As part of your mobile device management (MDM) solution, use these settings to mark rooted devices as not compliant, require device passwords, and more. As an Intune administrator, use these compliance settings to help protect your organization's resources. To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

Android AOSP devices are also governed by tenant-wide compliance policy settings. To manage the tenant-wide compliance policy settings in your tenant, sign in to Microsoft Endpoint Manager admin center and go to **Endpoint security** > **Device compliance** > **Compliance policy settings**.  

This feature applies to:

- Android Open Source Project  

## Before you begin  

[Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Android (AOSP)**.  

## Device Health  

- **Rooted devices**  
  Prevent rooted devices from having corporate access. 

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Mark rooted devices as not compliant.

## Device Properties

- **Maximum OS version**  
  When a device is using an OS version later than the version specified in the rule, access to company resources is blocked. The user is asked to contact their IT admin. Until a rule is changed to allow the OS version, this device can't access company resources.

  *By default, no version is configured*.

- **Minimum OS version**    
  When a device doesn't meet the minimum OS version requirement, it's reported as noncompliant. A link with information about how to upgrade is shown. The end user can choose to upgrade their device, and then get access to company resources.

  *By default, no version is configured*.  

- **Minimum security patch level**  
  Enter the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the `YYYY-MM-DD` format.

  *By default, no date is configured*.  

## System Security  

 - **Require a password on the device**  
 This setting specifies whether to require users to enter a password before access is granted to information on their mobile devices. 

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Require** - Users must enter a password on their device.  
  
  When set to *Require*, the following setting can be configured:  

  - **Required password type**  
  Require a password include only numeric characters, or a mix of numerals and other characters. 


    - **Device Default** - To evaluate password compliance, be sure to select a password strength other than **Device default**.
    - **Numeric**(*default) - Password must only be numbers, such as 123456789. Enter the minimum password length a user must enter, between 4 and 16 characters.  
     - **Numeric complex** - Repeated or consecutive numerals, such as `1111` or `1234`, aren't allowed.  


     > [!NOTE]  
     >- There is a known issue that prevents **Password required, no restriction** from working on AOSP devices.
     >- The following password types are listed as options but are not supported on AOSP devices: Alphabetic, alphanumeric, and alphanumeric with symbols.  


   - **Maximum minutes of inactivity before password is required**  
    Enter the maximum idle time allowed, from 1 minute to 8 hours, before the user must reenter their password to get back into their device. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.  
 
  - **Minimum password length**  
    Enter the minimum number of digits or characters that the password must have. Available for numeric or numeric complex password types.  

 ### Encryption

  - **Encryption of data storage on a device**  
    Your options are:  
 
    - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
    - **Require** - Encrypt data storage on your devices. Devices are encrypted when you choose the **Require a password to unlock mobile devices** setting.  

## Device compliance reporting  
Compliance reports are currently not available for AOSP devices. This section will be updated when reporting becomes available.   

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md).  
- [Set device restrictions for AOSP devices](../configuration/device-restrictions-android-aosp.md).  
