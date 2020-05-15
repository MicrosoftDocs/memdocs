---
# required metadata
title: Integrate Windows Hello for Business with Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn how to create a policy for controlling use of Windows Hello for Business on managed devices."
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/25/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
---

# Integrate Windows Hello for Business with Microsoft Intune  

You can integrate Windows Hello for Business (formerly Microsoft Passport for Work) with Microsoft Intune.

 Hello for Business is an alternative sign-in method that uses Active Directory or an Azure Active Directory account to replace a password, smart card, or a virtual smart card. It lets you use a *user gesture* to sign in, instead of a password. A user gesture might be a PIN, biometric authentication such as Windows Hello, or an external device such as a fingerprint reader.

Intune integrates with Hello for Business in two ways:

- An Intune policy can be created under **Device enrollment**. This policy targets the entire organization (tenant-wide). It supports the Windows AutoPilot out-of-box-experience (OOBE) and is applied when a device enrolls. 
- An identity protection profile can be created under **Device configuration**. This profile targets assigned users and devices, and is applied during check-in. 

Use this article to create a default Windows Hello for Business policy that targets your entire organization. To create an identity protection profile that is applied to select user and device groups, see [Configure an identity protection profile](identity-protection-configure.md).  

<!--- - You can store authentication certificates in the Windows Hello for Business key storage provider (KSP). For more information, see [Secure resource access with certificate profiles in Microsoft Intune](secure-resource-access-with-certificate-profiles.md). --->

> [!IMPORTANT]
> In Windows 10 desktop and mobile versions prior to the Anniversary Update, you could set two different PINS that could be used to authenticate to resources:
> - The **device PIN** could be used to unlock the device and connect to cloud resources.
> - The **work PIN** was used to access Azure AD resources on user's personal devices (BYOD).
> 
> In the Anniversary Update, these two PINS were merged into one single device PIN.
> Any Intune configuration policies you set to control the device PIN, and additionally, any Windows Hello for Business policies you configured, now both set this new PIN value.
> If you have set both policy types to control the PIN, the Windows Hello for Business policy is applied on both Windows 10 desktop and mobile devices.
> To ensure policy conflicts are resolved and that the PIN policy is applied correctly, update your Windows Hello for Business Policy to match the settings in your configuration policy, and ask your users to sync their devices in the Company Portal app.



## Create a Windows Hello for Business policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** >  **Enrollment** > **Enroll devices** > **Windows enrollment** > **Windows Hello for Business**. The Windows Hello for Business pane opens.

3. Select from the following options for **Configure Windows Hello for Business**:

    - **Disabled**. If you don't want to use Windows Hello for Business, select this setting. If disabled, users can't provision Windows Hello for Business except on Azure Active Directory joined mobile phones where provisioning may be required.
    - **Enabled**. Select this setting if you want to configure Windows Hello for Business settings.  When you select *Enabled*, additional settings for WIndows Hello become visible.
    - **Not configured**. Select this setting if you don't want to use Intune to control Windows Hello for Business settings. Any existing Windows Hello for Business settings on Windows 10 devices isn't changed. All other settings on the pane are unavailable.

4. If you selected **Enabled** in the previous step, configure the required settings that are applied to all enrolled Windows 10 and Windows 10 Mobile devices. After  you configure these settings, select **Save**.

   - **Use a Trusted Platform Module (TPM)**:

     A TPM chip provides an additional layer of data security. Choose one of the following values:

     - **Required** (default). Only devices with an accessible TPM can provision Windows Hello for Business.
     - **Preferred**. Devices first attempt to use a TPM. If this option isn't available, they can use software encryption.

   - **Minimum PIN length** and **Maximum PIN length**:

     Configures devices to use the minimum and maximum PIN lengths that you specify to help ensure secure sign-in. The default PIN length is six characters, but you can enforce a minimum length of four characters. The maximum PIN length is 127 characters.

   - **Lowercase letters in PIN**, **Uppercase letters in PIN**, and **Special characters in PIN**.

     You can enforce a stronger PIN by requiring the use of uppercase letters, lowercase letters, and special characters in the PIN. For each, select from:

     - **Allowed**. Users can use the character type in their PIN, but it isn't mandatory.

     - **Required**. Users must include at least one of the character types in their PIN. For example, it's common practice to require at least one uppercase letter and one special character.

     - **Not allowed** (default). Users must not use these character types in their PIN. (This is also the behavior if the setting isn't configured.)

       Special characters include: **! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~**

   - **PIN expiration (days)**:

     It's a good practice to specify an expiration period for a PIN, after which users must change it. The default is 41 days.

   - **Remember PIN history**:

     Restricts the reuse of previously used PINs. By default, the last 5 PINs can't be reused.

   - **Allow biometric authentication**:

     Enables biometric authentication, such as facial recognition or fingerprint, as an alternative to a PIN for Windows Hello for Business. Users must still configure a work PIN in case biometric authentication fails. Choose from:

     - **Yes**. Windows Hello for Business allows biometric authentication.
     - **No**. Windows Hello for Business prevents biometric authentication (for all account types).

   - **Use enhanced anti-spoofing, when available**:

     Configures whether the anti-spoofing features of Windows Hello are used on devices that support it. For example, detecting a photograph of a face instead of a real face.

     When set to **Yes**, Windows requires all users to use anti-spoofing for facial features when that is supported.

   - **Allow phone sign-in**:

     If this option is set to **Yes**, users can use a remote passport to serve as a portable companion device for desktop computer authentication. The desktop computer must be Azure Active Directory joined, and the companion device must be configured with a Windows Hello for Business PIN.

## Windows Holographic for Business support

Windows Holographic for Business supports the following settings for Windows Hello for Business:

- Use a Trusted Platform Module (TPM)
- Minimum PIN length
- Maximum PIN length
- Lowercase letters in PIN
- Uppercase letters in PIN
- Special characters in PIN
- PIN expiration (days)
- Remember PIN history

## Next steps

For more information about Windows Hello for Business, see [the guide](https://technet.microsoft.com/library/mt589441.aspx) in the Windows 10 documentation.
