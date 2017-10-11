---
title: "Windows Hello for Business settings"
titleSuffix: "Configuration Manager"
description: "Learn how to integrate Windows Hello for Business with System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
caps.latest.revision: 17
author: lleonard-msft
ms.author: alleonar
manager: angrobe

---
# Windows Hello for Business settings in System Center Configuration Manager (hybrid)

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager lets you integrate with Windows Hello for Business (formerly Microsoft Passport for Windows), which is an alternative sign-in method for Windows 10 devices. Hello for Business uses Active Directory, or an Azure Active Directory account to replace a password, smart card, or virtual smart card.  

Hello for Business lets you use a **user gesture** to login, instead of a password. A user gesture might be a simple PIN, biometric authentication, or an external device such as a fingerprint reader.  

 Configuration Manager integrates with Windows Hello for Business in two ways:  

-   You can use Configuration Manager to control which gestures users can and cannot use to sign in.  

-   You can store authentication certificates in the Windows Hello for Business key storage provider (KSP). For more information, see [Certificate profiles](create-pfx-certificate-profiles.md).  

- You can deploy Windows Hello for Business policies to domain-joined Windows 10 devices that run the Configuration Manager client. This configuration is described in [Configure Windows Hello for Business on domain-joined Windows 10 devices](../../protect/deploy-use/windows-hello-for-business-settings.md#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). When you are using Configuration Manager with Intune (hybrid), you can configure these settings on Windows 10, and Windows 10 Mobile devices, but not on domain-joined devices that run the Configuration Manager client.   

For general information about configuring Windows Hello for Business settings, see [Windows Hello for Business settings in System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md).

## Configure Windows Hello for Business settings (hybrid)  

1.  In the Configuration Manager console, click **Administration** > **Cloud Services** > **Microsoft Intune Subscriptions**.  

3.  From the list, select your Microsoft Intune subscription and then, in the **Home** tab, in the **Subscription** group, click **Configure Platforms** > **Windows (MDM)**.  

4.  On the **Windows Hello for Business** tab of the **Microsoft Intune Subscription Properties** dialog box, choose from the following values that will affect all enrolled Windows 10 and Windows 10 Mobile devices:  

    -   **Disable Windows Hello for Business on enrolled devices** or **Enable Windows Hello for Business on enrolled devices** - Enables or disables the use of Windows Hello for Business on all enrolled Windows 10 and Windows 10 Mobile devices.  

    -   **Use a Trusted Platform Module (TPM)** - A Trusted Platform Module (TPM) chip provides an additional layer of data security. Choose one of the following values:  

        -   **Required** (default) - Only devices with an accessible TPM can provision Windows Hello for Business.  

        -   **Preferred** - Devices first attempt to use a TPM. If this is not available, they can use software encryption  

    -   **Require minimum PIN length** - Specify the minimum number of characters required for the Windows Hello for Business PIN. You must use at least 4 characters (the default value is 6 characters).  

    -   **Require maximum PIN length** - Specify the maximum number of characters allowed for the Windows Hello for Business PIN. You can use up to 127 characters.  

    -   **Require lowercase letters in PIN** - Specifies whether lowercase letters must be used  in the Windows Hello for Business PIN. Choose from:  

        -   **Allowed** - Users can use lowercase characters in their PIN.  

        -   **Required** - Users must include at least one lowercase character in their PIN.  

        -   **Not allowed** (default) - Users must not use lowercase characters in their PIN.  

    -   **Require uppercase letters in PIN** - Specifies whether uppercase letters must be used  in the Windows Hello for Business PIN. Choose from:  

        -   **Allowed** - Users can use uppercase characters in their PIN.  

        -   **Required** - Users must include at least one uppercase character in their PIN.  

        -   **Not allowed** (default) - Users must not use uppercase characters in their PIN.  

    -   **Require special characters** - Specifies the use of special characters in the PIN. Choose from:  

        -   **Allowed** - Users can use special characters in their PIN.  

        -   **Required** - Users must include at least one special character in their PIN.  

        -   **Not allowed** (default) - Users must not use special characters in their PIN (this is also the behavior if the setting is not configured).  

         Special characters include: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **Require PIN expiration (days)** - Specifies the number of days before the device PIN must be changed. The default is 41 days.  

    -   **Prevent reuse of previous PINS** - Use this setting to restrict the re-use of previously used PINS. The default is the last 5 PINS used cannot be reused.  

    -   **Enable biometric gestures** - Enables biometric authentication such as facial recognition or fingerprint as an alternative to a PIN for Windows Hello for Business. Users must still configure a work PIN in case biometric authentication fails.  

         If set to **Enabled**, Windows Hello for Business allows biometric authentication.  If set to **Disabled**, Windows Hello for Business prevents biometric authentication (for all account types).  

    -   **Use enhanced anti-spoofing, when available** - Configures whether enhanced anti-spoofing is used on devices that support it.  

         If set to **Enabled**, Windows requires all users to use anti-spoofing for facial features when supported.  

    -   **Use Remote Passport** - If this option is set to **Enabled**, users can use a remote Hello for Business to serve as a portable companion device for desktop computer authentication. The desktop computer must be Azure Active Directory joined, and the companion device must be configured with a Windows Hello for Business PIN.  

5.  When you are finished, click **OK**.  

### See also  
 [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Manage identity verification using Windows Hello for Business](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  
