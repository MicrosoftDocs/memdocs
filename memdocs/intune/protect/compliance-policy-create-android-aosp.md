---
# required metadata

title: Android (AOSP) compliance settings in Microsoft Intune
description: View the Android (AOSP) device compliance settings available in Microsoft Intune.
keywords:
author: brenduns    
ms.author: brenduns
manager: dougeby
ms.date: 09/20/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345

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

# Device compliance settings for Android (AOSP) in Intune

This article lists the compliance settings you can configure for Android (AOSP) devices in Intune. Use these settings as part of your mobile device management (MDM) solution to define your organization's standards for:  

* Device health  
* Device properties  
* System security   

 Devices are also governed by tenant-wide compliance policy settings. To manage the tenant-wide compliance policy settings in your tenant, sign in to Microsoft Intune admin center and go to **Endpoint security** > **Device compliance** > **Compliance policy settings**.  

 To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).  

This feature applies to:

- Android (AOSP)

## Before you begin    

To access these settings, [create an Android (AOSP) compliance policy](create-compliance-policy.md#create-the-policy). When prompted to select a **Platform**, choose **Android (AOSP)**.  

## Device health  

- **Rooted devices**  
  Prevent rooted devices from having corporate access. 

  - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
  - **Block** - Mark rooted devices as not compliant.  

## Device properties  

- **Minimum OS version**    
  When a device doesn't meet the minimum OS version requirement, it's reported as noncompliant. A link with information about how to upgrade is shown. The end user can choose to upgrade their device, and then get access to company resources.  

  By default, no version is configured.  

- **Maximum OS version**  
  When a device is using an OS version later than the version specified in the rule, access to company resources is blocked. The user is asked to contact their IT admin. Until a rule is changed to allow the OS version, this device can't access company resources.

  By default, no version is configured.  

- **Minimum security patch level**  
  Enter the oldest security patch level a device can have. Devices that aren't at least at this patch level are noncompliant. The date must be entered in the `YYYY-MM-DD` format.

  By default, no patch level is configured.  

## System security  
 If you don't configure password requirements, the use of a device password is optional and left up to the users to configure.   

 - **Require a password to unlock mobile devices**  
    Require users to have a password-protected lock screen on their device. Your options:   

    - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.
    - **Yes** - Users must enter a password to unlock their devices.  
  
  If you require a password, also configure:   

  - **Required password type**  
      Require users to use a certain type of password. Your options:   

    - **Device default** - To evaluate password compliance, be sure to select a password strength other than **Device default**.  

    - **Numeric** - Password must only be numbers, such as `123456789`.  Also enter:  

      - Minimum password length: The minimum number of digits required, from 4 to 16.  

    - **Numeric complex** - Repeated or consecutive numerals, such as `1111` or `1234`, aren't allowed. Also enter:  

      - Minimum password length: The minimum number of digits required, from 4 to 16.  
 

    > [!NOTE]  
    >- There is a known issue that prevents **Password required, no restriction** from working on Android (AOSP) devices.  
    >- The following password types are listed as options but are not supported for Android (AOSP) devices: alphabetic, alphanumeric, and alphanumeric with symbols.  

  - **Maximum minutes of inactivity before password is required**  
      Enter the maximum idle time allowed, from 1 minute to 8 hours, before the user must re-enter their password to get back into their device. When you choose **Not configured** (default), this setting isn't evaluated for compliance or non-compliance.  

 ## Encryption  

  - **Encryption of data storage on a device**  
Your options are:  
 
    - **Not configured** (*default*) - This setting isn't evaluated for compliance or non-compliance.  

    - **Require** - Encrypt data storage on your devices. Devices are encrypted when you choose the **Require a password to unlock mobile devices** setting.  

## Device compliance reporting  
Compliance reports are currently not available for Android (AOSP) devices. This section will be updated when reporting becomes available.   

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md).  
- [Set device restrictions for AOSP devices](../configuration/device-restrictions-android-aosp.md).  
