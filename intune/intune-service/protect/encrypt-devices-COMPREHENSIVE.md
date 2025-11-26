---
title: Encrypt Windows devices with BitLocker using Intune
description: Use Microsoft Intune policy to manage BitLocker encryption on Windows devices, including silent encryption and Personal Data Encryption.
author: brenduns
ms.author: brenduns
ms.date: 11/26/2025
ms.topic: how-to
ms.reviewer: annovich; aanavath
ms.collection:
- M365-identity-device-management
- highpri
- highseo
- sub-secure-endpoints
---

# Encrypt Windows devices with BitLocker using Intune

Use Microsoft Intune to configure BitLocker encryption on devices that run Windows, and Personal Data Encryption (PDE) on devices that run Windows 11 Version 22H2 or later. This article covers both standard BitLocker encryption and silent BitLocker encryption scenarios.

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

## BitLocker encryption scenarios

Intune supports two primary BitLocker encryption approaches:

- **Standard BitLocker encryption** - Users may see prompts and can interact with the encryption process. Provides flexibility for encryption type selection and user-directed recovery key management.

- **Silent BitLocker encryption** - Automatic encryption without user interaction or administrative privileges required on the device. Ideal for organizations that want to ensure all managed devices are encrypted without depending on end-user action.

> [!TIP]
> Intune provides a built-in [encryption report](encryption-monitor.md) that presents details about the encryption status of devices across all your managed devices. After Intune encrypts a Windows device with BitLocker, you can view and manage BitLocker recovery keys when you view the encryption report.

## Prerequisites

### Licensing and Windows editions

For Windows editions that support BitLocker management, see [Windows edition and licensing requirements](/windows/security/operating-system-security/data-protection/bitlocker/configure?tabs=common#windows-edition-and-licensing-requirements) in the Windows documentation.

### Role-based access controls

To manage BitLocker in Intune, an account must be assigned an Intune [role-based access control](../fundamentals/role-based-access-control.md) (RBAC) role that includes the **Remote tasks** permission with the **Rotate BitLockerKeys (preview)** right set to **Yes**.

You can add this permission to your own [custom RBAC roles](../fundamentals/create-custom-role.md) or use one of the following [built-in RBAC roles](../fundamentals/role-based-access-control-reference.md):

- Help Desk Operator
- Endpoint Security Administrator

### Recovery planning

Before enabling BitLocker, understand and plan for recovery options that meet your organization's needs. For more information, see [BitLocker recovery overview](/windows/security/operating-system-security/data-protection/bitlocker/recovery-overview) in the Windows security documentation.

## Policy types for BitLocker encryption

Choose from the following Intune policy types to configure BitLocker encryption:

### Endpoint security policy (recommended)

**Endpoint security > Disk encryption policy** provides focused, security-specific BitLocker configuration:

- **BitLocker profile** - Dedicated settings for configuring BitLocker encryption. For more information, see the [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp).
- **Personal Data Encryption profile** - Configure PDE for file-level encryption that works alongside BitLocker for layered security. For more information, see the [PDE CSP](/windows/client-management/mdm/personaldataencryption-csp).

### Device configuration policy

**Device configuration > Endpoint protection profile** includes BitLocker settings as part of broader endpoint protection configuration. View available settings at [BitLocker in endpoint protection profiles](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!NOTE]
> **Settings Catalog limitations**: Settings Catalog doesn't include the necessary TPM startup authentication controls required for reliable silent BitLocker enablement. Use endpoint security or device configuration policies for BitLocker scenarios.

## Configure standard BitLocker encryption

Standard BitLocker encryption allows user interaction and provides flexibility for encryption configuration.

### Create endpoint security policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.

3. Set the following options:
   - **Platform**: Windows 10 and later
   - **Profile**: *BitLocker*

4. On the **Configuration settings** page, configure BitLocker settings for your business needs:
   - Configure encryption methods for OS, fixed, and removable drives
   - Set recovery options (password and key requirements)
   - Configure TPM startup authentication as needed

5. Complete the policy by assigning it to appropriate device groups.

### Create device configuration policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create**.

3. Set the following options:
   - **Platform**: **Windows 10 and later**
   - **Profile type**: Select **Templates** > **Endpoint protection**

4. On the **Configuration settings** page, expand **Windows Encryption** and configure BitLocker settings as needed.

5. Complete the policy by assigning it to appropriate device groups.

## Configure silent BitLocker encryption

Silent BitLocker encryption automatically encrypts devices without user interaction, providing a seamless encryption experience for managed environments.

### Prerequisites for silent encryption

#### Device requirements

A device must meet the following conditions for silent BitLocker enablement:

- **Operating System**:
  - If end users sign in as Administrators: Windows 10 version 1803 or later, or Windows 11
  - If end users sign in as Standard Users: Windows 10 version 1809 or later, or Windows 11

- **Device configuration**:
  - Microsoft Entra joined or Microsoft Entra hybrid joined
  - TPM (Trusted Platform Module) 1.2 or later
  - Native UEFI BIOS mode
  - [Secure Boot enabled](/troubleshoot/windows-client/windows-security/enforcing-bitlocker-policies-by-using-intune-known-issues#error-message-the-uefi-variable-secureboot-could-not-be-read)
  - [Windows Recovery Environment (WinRE) configured and available](/troubleshoot/windows-client/windows-security/enforcing-bitlocker-policies-by-using-intune-known-issues#event-id-854-winre-is-not-configured)

> [!NOTE]
> When BitLocker is enabled silently, the system automatically uses **full disk encryption** on non-modern standby devices and **used space only encryption** on modern standby devices. The encryption type depends on hardware capabilities and cannot be customized for silent encryption scenarios.

### Required settings for silent encryption

Configure the following settings depending on your chosen policy type:

#### Endpoint security policy for silent BitLocker

For **Endpoint security [Disk encryption](../protect/endpoint-security-disk-encryption-policy.md) policy**, configure these settings in the BitLocker profile:

- **Require Device Encryption** = *Enabled*
- **Allow Warning For Other Disk Encryption** = *Disabled*

> [!IMPORTANT]
> After setting **Allow Warning For Other Disk Encryption** to *Disabled*, another setting becomes available:
>
> - **Allow Standard User Encryption** = *Enabled*
>
> This setting is required if devices will be used by standard (non-administrator) users. It allows the RequireDeviceEncryption policy to work even when the current logged-on user is a standard user.

#### Device configuration policy for silent BitLocker

For **Device configuration [Endpoint protection](../protect/endpoint-protection-configure.md) policy**, configure these settings in the *Endpoint protection* template:

- **Warning for other disk encryption** = *Block*
- **Allow standard users to enable encryption during Microsoft Entra join** = *Allow*
- **User creation of recovery key** = *Allow* or *Do not allow 256-bit recovery key*
- **User creation of recovery password** = *Allow* or *Require 48-digit recovery password*

### TPM startup authentication for silent encryption

For silent BitLocker to work, devices **must not require** TPM startup PIN or startup key, as these require user interaction.

#### Configure TPM settings

Configure TPM startup authentication settings to prevent user interaction:

**Endpoint security policy** - In the BitLocker profile, expand *Administrative Templates* > *Windows Components* > *BitLocker Drive Encryption* > *Operating System Drives* and set *Require additional authentication at startup* to *Enabled*. Then configure:

- **Configure TPM startup PIN** = *Do not allow startup PIN with TPM*
- **Configure TPM startup key** = *Do not allow startup key with TPM*
- **Configure TPM startup key and PIN** = *Do not allow startup key and PIN with TPM*
- **Configure TPM startup** = *Allow TPM* or *Require TPM*

**Device configuration policy** - In the endpoint protection template under *Windows Encryption*:

- **Compatible TPM startup** = *Allow TPM* or *Require TPM*
- **Compatible TPM startup PIN** = *Do not allow startup PIN with TPM*
- **Compatible TPM startup key** = *Do not allow startup key with TPM*
- **Compatible TPM startup key and PIN** = *Do not allow startup key and PIN with TPM*

> [!WARNING]
> Security baselines, particularly the Microsoft Defender for Endpoint baseline, can enable TPM startup PIN and key by default, which blocks silent enablement. Review your baseline configurations for conflicts and reconfigure or exclude devices as needed.

## Encryption type behavior

The encryption type (full disk vs. used space only) is determined by:

1. **Hardware capabilities** - Whether the device supports [modern standby](/windows-hardware/design/device-experiences/modern-standby)
2. **Silent encryption configuration** - Whether silent enablement is configured
3. **SystemDrivesEncryptionType setting** - If explicitly configured

### Default behavior

When SystemDrivesEncryptionType isn't configured:

- **Modern standby devices with silent encryption** = Used space only encryption
- **Non-modern standby devices with silent encryption** = Full disk encryption
- **Standard (non-silent) encryption** = User can choose or policy-defined

### Verify device capabilities

To check if a device supports modern standby, run from a command prompt:

```console
powercfg /a
```

**Modern standby capable**: Shows "Standby (S0 Low Power Idle) Network Connected" is available
**Not modern standby capable**: Shows "Standby (S0 Low Power Idle) Network Connected" is not supported

### Verify encryption type

To check the current encryption type, run from an elevated command prompt:

```console
manage-bde -status c:
```

The 'Conversion Status' field shows either "Used Space Only Encrypted" or "Fully Encrypted".

## Personal Data Encryption (PDE)

Personal Data Encryption provides file-level encryption that complements BitLocker:

- **PDE encrypts files** instead of whole volumes
- **Works alongside BitLocker** for layered security
- **Requires Windows Hello for Business** sign-in to release encryption keys
- **Available on Windows 11 22H2 or later**

To configure PDE, use either:
- **Endpoint security policy** with the *Personal Data Encryption* profile
- **Settings Catalog** with the *PDE* category

## Monitor and manage BitLocker

### View encryption status

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Encryption report**.

2. Review the encryption status of devices that received BitLocker policies.

3. Access BitLocker recovery keys and device compliance information.

### Recovery key management

#### View recovery keys

BitLocker recovery keys are automatically backed up to Microsoft Entra ID when encryption occurs:

1. **For Intune-managed devices**: Use the encryption report in Intune admin center
2. **For Microsoft Entra joined devices**: Access through Microsoft Entra ID or user self-service

#### Rotate recovery keys

Use the **Rotate BitLocker Keys** remote action to refresh recovery passwords on Microsoft Entra joined and hybrid joined devices.

#### Self-service recovery

End users can access their own BitLocker recovery keys through:
- **My Account portal** (account.microsoft.com)
- **Microsoft Entra joined devices**: Direct access through Microsoft Entra ID

## Troubleshooting

### Common issues for silent BitLocker

**Issue**: BitLocker requires user interaction despite silent configuration

- **Solution**: Verify TPM startup PIN or key settings aren't enabled. Check for conflicting security baseline policies.

**Issue**: Devices don't meet prerequisites for silent enablement

- **Solution**: Verify devices meet all device prerequisites, including TPM version, UEFI mode, and Microsoft Entra join status.

**Issue**: BitLocker fails to encrypt silently

- **Solution**: Check Windows event logs for BitLocker-related errors. Verify Secure Boot is enabled and WinRE is properly configured.

**Issue**: Policy conflicts prevent silent enablement

- **Solution**: Use [policy conflict detection](../configuration/device-profile-monitor.md#view-conflicts) in Intune to identify conflicting settings between policies.

### Recovery key troubleshooting

For silent BitLocker enablement, recovery keys are automatically backed up to Microsoft Entra ID when encryption occurs. Verify:

1. Devices are successfully Microsoft Entra joined (required for automatic backup)
2. No policy conflicts prevent the automatic backup process
3. Recovery key escrow is functioning through the encryption report

## Next steps

- [Monitor disk encryption](../protect/encryption-monitor.md)
- [Troubleshooting BitLocker policy](/troubleshoot/mem/intune/troubleshoot-bitlocker-policies)
- [BitLocker deployment comparison chart](/windows/security/information-protection/bitlocker/bitlocker-deployment-comparison)
- [Known issues for BitLocker policies](/windows/security/information-protection/bitlocker/ts-bitlocker-intune-issues)