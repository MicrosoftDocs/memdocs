---
# required metadata

title: Windows Hello for Business settings in Microsoft Intune
description: View details for Windows Hello for Business settings you configure in an Intune identity protection profile for device groups in Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/09/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- identity-protection
- sub-secure-endpoints

ms.reviewer: mattcall

---

# Identity protection profile settings in Intune for Windows Hello for Business

> [!IMPORTANT]
>
> In July 2024, the following Intune profiles for identity protection and account protection were deprecated and replaced by a new consolidated profile named *Account protection*. This newer profile is found in the account protection policy node of endpoint security, and is the only profile template that remains available to create new policy instances for identity and account protection. The settings from this new profile are also available through the settings catalog.
>
> Any instances of the following older profiles that you have created remain available to use and edit:
>
> - **Identity protection** – previously available from *Devices* > *Configuration* > *Create* > *New Policy* > *Windows 10 and later* > *Templates* > *Identity Protection*
> - **Account protection (Preview)** – previously available from *Endpoint Security* > *Account protection* > *Windows 10 and later* > *Account protection ( Preview)*

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article describes Windows Hello for Business settings you can manage with an Identity protection profile. Identity protection profiles are part of device configuration policy in Microsoft Intune. However, as of July 2024, device configuration profiles for *Identity protection* are replaced by endpoint security profiles for *Account protection*. While you can continue to use identity protection profiles that you previously created, Intune no longer supports creating new instances. Instead, to manage settings for identity protection, use an endpoint security [account protection policy](../protect/endpoint-security-account-protection-policy.md).

With an Identity protection profile, you can configure settings on discrete groups of Windows 10/11 devices. To configure Windows Hello for Business tenant-wide, as part of *device enrollment*, see [Create a Windows Hello for Business policy](../protect/windows-hello.md) in *Integrate Windows Hello for Business with Microsoft Intune*.

This article describes the settings for the enrollment policy.

You can find additional information about these settings in [Configure Windows Hello for Business Policy settings](/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings), in the Windows Hello documentation.

## Windows Hello for Business

*The following settings details apply only to the device configuration profile template for Identity protection, which was deprecated in July 2024.*

- **Configure Windows Hello for Business**:  

  - **Not configured** (*default*) - Select this setting if you don't want to use Intune to control Windows Hello for Business settings. Any existing Windows Hello for Business settings on Windows 10/11 devices isn't changed. All other settings on the pane are unavailable.

  - **Disable** - If you don't want to use Windows Hello for Business, select this setting. All other settings on the screen are then unavailable.
  - **Enable** - Select this setting if you want to configure Windows Hello for Business settings.

  When set to *Enable*, the following settings are available:

  - **Minimum PIN length**  
    Specify a minimum PIN length for devices, from 4 to 127 characters. By default, this setting is *Not configured*.

  - **Maximum PIN length**  
  Specify a maximum PIN length for devices, from four to 127 characters. By default, this setting is *Not configured*.

  - **Lowercase letters in PIN**  
    If required, user PIN must include at least one lowercase letter. By default, this setting is *Not configured*.

    - **Not allowed** - Block users from using lowercase letters in the PIN. This behavior also occurs if the setting isn't configured.
    - **Allowed** - Allow users to use lowercase letters in the PIN, but it's not required.
    - **Required** - Users must include at least one lowercase letter in the PIN. For example, it's common practice to require at least one uppercase letter and one special character.

  - **Uppercase letters in PIN**  
    If required, user PIN must include at least one uppercase letter. By default, this setting is *Not configured*.

    - **Not allowed** - Block users from using uppercase letters in the PIN. This behavior also occurs if the setting isn't configured.
    - **Allowed** - Allow users to use uppercase letters in the PIN, but it's not required.
    - **Required** - Users must include at least one uppercase letter in the PIN. For example, it's common practice to require at least one uppercase letter and one special character.

  - **Special characters in PIN**  
    If required, user PIN must include at least one special character. Special characters include: `! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~`

    - **Not allowed** (*default*) - Block users from using special characters in the PIN. This behavior also occurs if the setting isn't configured.
    - **Allowed** - Allow users to use uppercase letters in the PIN, but it's not required.
    - **Required** - Users must include at least one uppercase letter in the PIN. For example, it's common practice to require at least one uppercase letter and one special character.

  - **PIN expiration (days)**  
    If configured, the user will be forced to change their PIN after the set number of days. The user can still proactively change their PIN before expiration. By default, this setting is *Not configured*.

  - **Remember PIN history**  
    If configured, the user will not be able to reuse this number of previous PINs. By default, this setting is *Not configured*.

  - **Enable PIN recovery**  
    Allows user to use the Windows Hello for Business PIN recovery service.

    - **Enable** - The PIN recovery secret is stored on the device and the user can change their PIN if needed.
    - **Not configured** (*default*) - The recovery secret isn't created or stored.

  - **Use a Trusted Platform Module (TPM)**  
    A TPM chip provides an additional layer of data security.

    - **Enable** - Only devices with an accessible TPM can provision Windows Hello for Business.
    - **Not configured** (*default*) - Devices first attempt to use a TPM. If a TPM isn't available, they can use software encryption.

  - **Allow biometric authentication**  
    If allowed, Windows Hello for Business can authenticate using gestures, such as face and fingerprint. Users must still configure a PIN in case of failure.

    - **Enable** - Windows Hello for Business allows biometric authentication.
    - **Not configured** (*default*) - Windows Hello for Business prevents biometric authentication (for all account types).

  - **Use enhanced anti-spoofing, when available**  
    If enabled, devices use enhanced anti-spoofing, when available (for example, detecting a photograph of a face instead of a real face).

    - **Enable** - Windows requires all users to use anti-spoofing for facial features when that is supported.
    - **Not configured** (*default*) - Windows honors the anti-spoofing configurations on the device.

  - **Certificate for on-premise resources**  

    - **Enable** - Allows Windows Hello for Business to use certificates to authenticate to resources on-premises.
    - **Not configured** (*default*) - Prevents Windows Hello for Business from using certificates to authenticate to resources on-premises. Instead, devices use the default behavior of *key-trust on-premises authentication*. For more information, see [User certificate for on-premises authentication](/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings#use-certificate-for-on-premises-authentication) in the Windows Hello documentation.

- **Use security keys for sign-in**  
  This setting is available for devices that run Windows 10 version 1903 or later, or Windows 11. Use it to manage support for using Windows Hello security keys for sign-in.

  - **Enable** - Users can use a Windows Hello security key as a sign-in credential for PCs targeted with this policy.
  - **Not configured** - Security keys are disabled and users can't use them to sign in to PCs.

## Next steps

[Assign the profile](../configuration/device-profile-assign.md) and [monitor its status](../configuration/device-profile-monitor.md)