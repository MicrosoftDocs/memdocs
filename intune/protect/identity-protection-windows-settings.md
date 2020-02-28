---
# required metadata

title: Windows Hello for Business settings in Microsoft Intune - Azure | Microsoft Docs
description: See a list of all the PIN, biometric, and anti-spoofing settings in an identity protection profile to use and configure Windows Hello for Business on Windows 10 devices in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/20/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate

---

# Windows 10 device settings to enable Windows Hello for Business in Intune

This article lists and describes the Windows Hello for Business settings you can control on Windows 10 devices in Intune. As an Intune administrator, you can configure and assign these settings to Windows 10 devices as part of your mobile device management (MDM) solution. 

You can find additional information about these settings in [Configure Windows Hello for Business Policy settings](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings), in the Windows Hello documentation.


To learn more about Windows Hello for Business profiles in Intune, see [configure identity protection](identity-protection-configure.md).

## Before you begin

[Create a configuration profile](identity-protection-configure.md#create-the-device-profile).

## Windows Hello for Business
- **Configure Windows Hello for Business**:
  - **Not configured** - Select this setting if you don't want to use Intune to control Windows Hello for Business settings. Any existing Windows Hello for Business settings on Windows 10 devices is not changed. All other settings on the pane are unavailable.

  - **Disabled** - If you don't want to use Windows Hello for Business, select this setting. All other settings on the screen are then unavailable.
  - **Enabled** - Select this setting if you want to configure Windows Hello for Business settings.  
  
  **Default**: Not configured

  When set to *Enabled*, the following settings are available:

  - **Minimum PIN length**  
    Specify a minimum PIN length for devices, to help secure sign-in. Windows device defaults are six characters, but this setting can enforce a minimum of four to 127 characters. 

    **Default**: *Not configured*

  - **Maximum PIN length**  
  Specify a maximum PIN length for devices, to help secure sign-in. Windows device defaults are six characters, but this setting can enforce a minimum of four to 127 characters.  

    **Default**: *Not configured*  

  - **Lowercase letters in PIN**  
    You can enforce a stronger PIN by requiring end users include lowercase letters. Your options:

    - **Not allowed** - Block users from using lowercase letters in the PIN. This behavior also occurs if the setting isn't configured.
    - **Allowed** - Allow users to use lowercase letters in the PIN, but it's not required.
    - **Required** - Users must include at least one lowercase letter in the PIN. For example, it's common practice to require at least one uppercase letter and one special character.

  - **Uppercase letters in PIN**  
    You can enforce a stronger PIN by requiring end users include uppercase letters. Your options:

    - **Not allowed** - Block users from using uppercase letters in the PIN. This behavior also occurs if the setting isn't configured.
    - **Allowed** - Allow users to use uppercase letters in the PIN, but it's not required.
    - **Required** - Users must include at least one uppercase letter in the PIN. For example, it's common practice to require at least one uppercase letter and one special character.

  - **Special characters in PIN**  
    You can enforce a stronger PIN by requiring end users include special characters. Special characters include: `! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~`  

    Your options:
    - **Not allowed** - Block users from using special characters in the PIN. This behavior also occurs if the setting isn't configured.
    - **Allowed** - Allow users to use uppercase letters in the PIN, but it's not required.
    - **Required** - Users must include at least one uppercase letter in the PIN. For example, it's common practice to require at least one uppercase letter and one special character.

    **Default**: Not allowed

  - **PIN expiration (days)**  
    It's a good practice to specify an expiration period for a PIN, after which users must change it. Windows device defaults are 41 days.

    **Default**: Not Configured

  - **Remember PIN history**  
    Restricts the reuse of previously used PINs. Windows devices default to preventing reuse of the last five PINs.  

    **Default**: Not Configured  

  - **Enable PIN recovery**   
    Allows user to use the Windows Hello for Business PIN recovery service. 
    
    - **Enabled** - The PIN recovery secret is stored on the device and the user can change their PIN if needed.  
    - **Disabled** - The recovery secret isn't created or stored.

    **Default**: Not configured

  - **Use a Trusted Platform Module (TPM)**   
    A TPM chip provides an additional layer of data security.  

    - **Enabled** - Only devices with an accessible TPM can provision Windows Hello for Business.
    - **Not configured** - Devices first attempt to use a TPM. If this is not available, they can use software encryption.
    
    **Default**: Not configured

  - **Allow biometric authentication**  
     Enables biometric authentication, such as facial recognition or fingerprint, as an alternative to a PIN for Windows Hello for Business. Users must still configure a work PIN in case biometric authentication fails. Choose from:

    - **Enable** - Windows Hello for Business allows biometric authentication.
    - **Not configured** - Windows Hello for Business prevents biometric authentication (for all account types).

    **Default**: Not configured

  - **Use enhanced anti-spoofing, when available**  
    Configures whether the anti-spoofing features of Windows Hello are used on devices that support it (for example, detecting a photograph of a face instead of a real face).  
    - **Enable** - Windows requires all users to use anti-spoofing for facial features when that is supported.
    - **Not configured** - Windows honors the anti-spoofing configurations on the device.

    **Default**: Not configured

  - **Certificate for on-premise resources**  

    - **Enable** - Allows Windows Hello for Business to use certificates to authenticate to resources on-premises.
    - **Not configured** - Prevents Windows Hello for Business from using certificates to authenticate to resources on-premises. Instead, devices use the default behavior of *key-trust on-premises authentication*. For more information, see [User certificate for on-premises authentication](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings#use-certificate-for-on-premises-authentication) in the Windows Hello documentation.  

  **Default**: Not configured

- **Use security keys for sign-in**  
  This setting is available for devices that run Windows 10 version 1903 or later. Use it to manage support for using Windows Hello security keys for sign-in.  

  - **Enabled** - Users can use a Windows Hello security key as a logon credential for PCs targeted with this policy. 
  - **Disabled** - Security keys are disabled and users cannot use them to sign in to PCs.   

  **Default**: Not configured

## Next steps

[Assign the profile](../configuration/device-profile-assign.md) and [monitor its status](../configuration/device-profile-monitor.md).
