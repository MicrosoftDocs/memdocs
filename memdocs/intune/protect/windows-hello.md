---
# required metadata
title: Configure a tenant-wide Windows Hello for Business policy with Microsoft Intune
titleSuffix: Microsoft Intune
description: Apply policy for Windows Hello for Business on devices at the time they enroll with Microsoft Intune
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/23/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- identity-protection
- sub-secure-endpoints

ms.reviewer: shpate
---

# Configure Windows Hello for Business on devices when they enroll with Intune

With Microsoft Intune, you can create a tenant-wide policy that configures use of Windows Hello for Business on Windows 10 or Windows 11 devices at the time those devices enroll with Intune. This policy targets your entire organization and supports the Windows Autopilot out-of-box-experience (OOBE).

For Windows 10/11 devices, use of [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview) replaces the use of passwords with strong two-factor authentication on devices. This authentication consists of a user credential that’s tied to a device and uses a biometric or PIN.

After device enrollment, or when you choose not to use the tenant-wide enrollment policy, Intune supports the following methods to manage Windows Hello on discrete groups of devices:

- [**Endpoint security Account protection policy**](../protect/endpoint-security-account-protection-policy.md): To manage settings for Windows Hello on devices after they have enrolled with Intune, use the Intune *Account protection* profile, which is part of endpoint security Account protection policy.

- [**Security baselines**](../protect/security-baselines.md): Some settings for Windows Hello can be managed by security baselines like the baselines for *Microsoft Defender for Endpoint security* or *Security Baseline for Windows 10 and later*.

- [**Settings catalog**](../configuration/settings-catalog.md): The settings from endpoint security Account protection profiles are available in the Intune settings catalog.

> [!IMPORTANT]
> Prior to the Anniversary Update (Windows version 1607), you could set two different PINS that could be used to authenticate to resources:
>
> - The device PIN could be used to unlock the device and connect to cloud resources.
> - The work PIN was used to access Microsoft Entra resources on a user's personal device (BYOD).
>
> In the Anniversary Update, these two PINS were merged into one single device PIN.
> Any Intune configuration policies you set to control the device PIN, and additionally, any Windows Hello for Business policies you configured, now both set this new PIN value.
> If you have set both policy types to control the PIN, the Windows Hello for Business policy is applied.
> To ensure policy conflicts are resolved and that the PIN policy is applied correctly, update your Windows Hello for Business Policy to match the settings in your configuration policy, and ask your users to sync their devices in the Company Portal app.

## Role-based access control

You must be an Intune Service Administrator to create or edit a Windows Hello for Business policy in Windows enrollment. All other Intune roles have read-only access. For more information about role-based access control (RBAC), see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Create a Windows Hello for Business policy for device enrollment

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **Enrollment**.

3. In the **Windows** tab, under **Enrollment options**, select **Windows Hello for Business**. Wait while the Windows Hello for Business pane opens.

4. Select from the following options for **Configure Windows Hello for Business**:

   - **Enabled**. Select this setting if you want to configure Windows Hello for Business settings. When you select *Enabled*, other settings for Windows Hello are visible and can be configured for devices.

   - **Disabled**. If you don't want to enable Windows Hello for Business during device enrollment, select this option. When disabled, users can't provision Windows Hello for Business. When set to *Disabled*, you can still configure the subsequent settings for Windows Hello for Business even though this policy won't enable Windows Hello for Business.

   - **Not configured**. Select this setting if you don't want to use Intune to control Windows Hello for Business settings. Any existing Windows Hello for Business settings on Windows 10/11 devices don't change. All other settings on the pane are unavailable.

5. If you selected **Enabled** in the previous step, configure the required settings that are applied to all enrolled Windows 10/11 devices. After you configure these settings, select **Save**.

   - **Use a Trusted Platform Module (TPM)**:

     A TPM chip provides another layer of data security. Choose one of the following values:

     - **Required** (default). Only devices with an accessible TPM can provision Windows Hello for Business.
     - **Preferred**. Devices first attempt to use a TPM. If this option isn't available, they can use software encryption.

   - **Minimum PIN length** and **Maximum PIN length**:

     Configures devices to use the minimum and maximum PIN lengths that you specify to help ensure secure sign-in. The default PIN length is six characters, but you can enforce a minimum length of four characters. The maximum PIN length is 127 characters.

   - **Lowercase letters in PIN**, **Uppercase letters in PIN**, and **Special characters in PIN**.

     You can enforce a stronger PIN by requiring the use of uppercase letters, lowercase letters, and special characters in the PIN. For each, select from:

     - **Allowed**: Users can use the character type in their PIN, but it isn't mandatory.

     - **Required**: Users must include at least one of the character types in their PIN. For example, it's common practice to require at least one uppercase letter and one special character.

     - **Not allowed** (default): Users must not use these character types in their PIN. (This is also the behavior if the setting isn't configured.)

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

     If this option is set to **Yes**, users can use a remote passport to serve as a portable companion device for desktop computer authentication. The desktop computer must be Microsoft Entra joined, and the companion device must be configured with a Windows Hello for Business PIN.

   - **Enable enhanced sign in security**:

      Configure [Windows Hello Enhanced Sign-in Security](/windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security) on devices with capable hardware. Your options:

      - **Enhanced sign-in security will be enabled on systems with capable hardware** (default): Device users can't use external peripherals to sign in to their device with Windows Hello.
      - **Enhanced sign-in security will be disabled on all systems**: Device users can use external peripherals that are compatible with Windows Hello to sign in to their device.

   - **Use security keys for sign-in**:

     When set to **Enabled**, this setting provides the capacity for remotely turning ON/OFF Windows Hello Security Keys for all computers in a customer's organization.

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

Learn more about Windows Hello from the following subjects in the Windows documentation:

- [Planning a Windows Hello for Business deployment](/windows/security/identity-protection/hello-for-business/hello-planning-guide)
- [Windows Hello for Business Deployment Prerequisite Overview](/windows/security/identity-protection/hello-for-business/hello-identity-verification)
