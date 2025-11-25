---
title: Silently enable BitLocker on Windows devices with Intune
description: Learn how to configure BitLocker encryption to automatically and silently encrypt devices without user interaction using Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 11/24/2025
ms.topic: how-to
ms.reviewer: annovich; aanavath
ms.collection:
- M365-identity-device-management
- highpri
- highseo
- sub-secure-endpoints
---

# Silently enable BitLocker on devices with Intune

You can configure a BitLocker policy to automatically and silently encrypt a device without presenting any UI to the end user, even when that user isn't a local Administrator on the device.

Silent enablement of BitLocker provides a seamless encryption experience that doesn't require user interaction or administrative privileges on the device. This approach is ideal for organizations that want to ensure all managed devices are encrypted without depending on end-user action.

This article shows you how to configure silent BitLocker enablement, including:

- Device prerequisites for silent encryption
- Required policy settings for both endpoint security and device configuration policies
- TPM configuration requirements
- Troubleshooting common issues

To learn about general BitLocker management and other encryption options, see [Manage Disk Encryption policy for Windows devices with Intune](encrypt-devices.md).

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

## Prerequisites

### Device Prerequisites

A device must meet the following conditions to be eligible for silently enabling BitLocker:

- If end users sign in to the devices as Administrators, the device must run Windows 10 version 1803 or later, or Windows 11.
- If end users sign in to the devices as Standard Users, the device must run Windows 10 version 1809 or later, or Windows 11.
- The device must be Microsoft Entra joined or Microsoft Entra hybrid joined.
- Device must contain at least TPM (Trusted Platform Module) 1.2.
- The BIOS mode must be set to Native UEFI only.
- Secure Boot [must be enabled](/troubleshoot/windows-client/windows-security/enforcing-bitlocker-policies-by-using-intune-known-issues#error-message-the-uefi-variable-secureboot-could-not-be-read).
- Windows Recovery Environment (WinRE) is [configured and available](/troubleshoot/windows-client/windows-security/enforcing-bitlocker-policies-by-using-intune-known-issues#event-id-854-winre-is-not-configured).

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

### Licensing and permissions

For Windows editions that support BitLocker management, see [Windows edition and licensing requirements](/windows/security/operating-system-security/data-protection/bitlocker/configure?tabs=common#windows-edition-and-licensing-requirements) in the Windows documentation.

To manage BitLocker in Intune, an account must be assigned an Intune [role-based access control](../fundamentals/role-based-access-control.md) (RBAC) role that includes the **Remote tasks** permission with the **Rotate BitLockerKeys (preview)** right set to **Yes**. For more information, see the [BitLocker management prerequisites](encrypt-devices.md#prerequisites).

## Configure silent BitLocker enablement

To successfully enable BitLocker silently, devices must receive the applicable settings and must not have settings that require use of a TPM startup PIN or key. Use of a startup PIN or key is incompatible with silent encryption as it requires user interaction.

### Required settings to silently enable BitLocker

Depending on the type of policy that you use to silently enable BitLocker, configure the following settings. Both methods manage BitLocker through Windows encryption CSPs on Windows devices.

# [Endpoint security policy](#tab/endpoint-security)

For **Endpoint security [Disk encryption](../protect/endpoint-security-disk-encryption-policy.md) policy**, configure the following settings in the BitLocker profile:

- **Require Device Encryption** = *Enabled*
- **Allow Warning For Other Disk Encryption** = *Disabled*

:::image type="content" source="./media/encrypt-devices/silent-encryption-configuration.png" alt-text="Two BitLocker settings required to enable silent encryption.":::

In addition to the two required settings, consider use of *[Configure Recovery Password Rotation](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#configurerecoverypasswordrotation)*.

# [Device configuration policy](#tab/device-configuration)

For **Device configuration [Endpoint protection](../protect/endpoint-protection-configure.md) policy**, configure the following settings in the *Endpoint protection* template or a *custom settings* profile:

- **Warning for other disk encryption** = *Block*
- **Allow standard users to enable encryption during Microsoft Entra join** = *Allow*
- **User creation of recovery key** = *Allow or Do not allow 256-bit recovery key*
- **User creation of recovery password** = *Allow or Require 48-digit recovery password*

---

### TPM startup PIN or key configuration

A device **must not be set to require** a startup PIN or startup key for silent enablement to work.

When a TPM startup PIN or startup key is required on a device, BitLocker can't silently enable on the device, and instead requires interaction from the end user. Settings to configure the TPM startup PIN or key are available in both the endpoint protection template and the BitLocker policy. By default, these policies don't configure these settings.

> [!TIP]
> Be aware of policies that might enable use of a TPM startup PIN or key. For example, Intune security baselines like the Microsoft Defender for Endpoint baseline can enable a TPM startup PIN and key by default, blocking silent enablement of BitLocker. [Review policies](/intune/intune-service/configuration/device-profile-monitor?tabs=policy%2Cdevices#view-conflicts) for conflicts.

Following are the relevant settings for each profile type:

# [Endpoint security policy](#tab/endpoint-security-tpm)

**Endpoint security disk encryption policy** - TPM settings are only visible after you expand the *Administrative Templates* category and then in the *Windows Components > BitLocker Drive Encryption > Operating System Drives* section set *Require additional authentication at startup* to *Enabled*. When configured, the following TPM settings are then available:

- **Configure TPM startup key and PIN** - Configure this as *Do not allow startup key and PIN with TPM*
- **Configure TPM startup PIN** - Configure this as *Do not allow startup PIN with TPM*
- **Configure TPM startup** - Configure this as *Allow TPM* or *Require TPM*
- **Configure TPM startup key** - Configure this as *Do not allow startup key with TPM*

# [Device configuration policy](#tab/device-configuration-tpm)

**Device configuration policy** - In the endpoint protection template you'll find the following settings in the *Windows Encryption* category:

- **Compatible TPM startup** - Configure this as *Allow TPM* or *Require TPM*
- **Compatible TPM startup PIN** - Configure this as *Do not allow startup PIN with TPM*
- **Compatible TPM startup key** - Configure this as *Do not allow startup Key with TPM*
- **Compatible TPM startup key and PIN** - Configure this as *Do not allow startup Key and PIN with TPM*

---

> [!WARNING]
> While neither the endpoint security or device configuration policies configure the TPM settings by default, some versions of the [security baseline for Microsoft Defender for Endpoint](../protect/security-baselines.md#available-security-baselines) will configure both *Compatible TPM startup PIN* and *Compatible TPM startup key* by default. These configurations might block silent enablement of BitLocker.
>
> If you deploy this baseline to devices on which you want to silently enable BitLocker, review your baseline configurations for possible conflicts. To remove conflicts, either reconfigure the settings in the baselines to remove the conflict, or remove applicable devices from receiving the baseline instances that configure TPM settings that block silent enablement of BitLocker.

## Create and deploy silent BitLocker policy

Use the following procedures to create a policy that silently enables BitLocker.

### Create endpoint security policy for silent BitLocker

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.

3. Set the following options:
   1. **Platform**: Windows
   2. **Profile**: *BitLocker*

4. On the **Configuration settings** page, configure the following settings:
   - **Require Device Encryption** = *Enabled*
   - **Allow Warning For Other Disk Encryption** = *Disabled*

5. Configure any additional BitLocker settings as needed for your organization.

6. Ensure TPM startup PIN and key settings are configured to not require user interaction (see [TPM startup PIN or key configuration](#tpm-startup-pin-or-key-configuration)).

7. Complete the policy creation by assigning it to the appropriate device groups.

### Create device configuration policy for silent BitLocker

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create**.

3. Set the following options:
   1. **Platform**: **Windows 10 and later**
   2. **Profile type**: Select **Templates** > **Endpoint protection**

4. On the **Configuration settings** page, expand **Windows Encryption** and configure:
   - **Warning for other disk encryption** = *Block*
   - **Allow standard users to enable encryption during Microsoft Entra join** = *Allow*
   - **User creation of recovery key** = *Allow or Do not allow 256-bit recovery key*
   - **User creation of recovery password** = *Allow or Require 48-digit recovery password*

5. Configure TPM settings to not require startup PIN or key (see [TPM startup PIN or key configuration](#tpm-startup-pin-or-key-configuration)).

6. Complete the policy creation by assigning it to the appropriate device groups.

## Verify silent BitLocker enablement

After deploying a silent BitLocker policy, you can verify that devices are being encrypted without user interaction.

### Check device encryption status

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Encryption report**.

2. Review the encryption status of devices that received the silent BitLocker policy.

3. For devices that show as encrypted, you can verify the encryption occurred silently by checking that no user interaction was required.

### Verify encryption type

To verify the encryption type on a device, run the following command from an elevated command prompt:

```console
manage-bde -status c:
```

The output shows whether the device used "Used Space Only Encrypted" or "Fully Encrypted" based on the device capabilities and policy configuration.

## Troubleshoot silent BitLocker enablement

### Common issues and solutions

**Issue**: BitLocker requires user interaction despite silent configuration
- **Solution**: Verify that TPM startup PIN or key settings are not enabled. Check for conflicting security baseline policies.

**Issue**: Devices don't meet prerequisites for silent enablement
- **Solution**: Verify devices meet all [device prerequisites](#device-prerequisites), including TPM version, UEFI mode, and Microsoft Entra join status.

**Issue**: BitLocker fails to encrypt silently
- **Solution**: Check Windows event logs for BitLocker-related errors. Verify that Secure Boot is enabled and WinRE is properly configured.

**Issue**: Policy conflicts prevent silent enablement
- **Solution**: Use the [policy conflict detection](../../intune-service/configuration/device-profile-monitor.md#view-conflicts) feature in Intune to identify conflicting settings between different policies.

### Recovery key escrow verification

For silent BitLocker enablement, ensure recovery keys are properly escrowed:

1. Verify that **Save BitLocker recovery information to Microsoft Entra ID** is enabled
2. Check that **Store recovery information in Microsoft Entra ID before enabling BitLocker** is configured as required
3. Monitor the [encryption report](encryption-monitor.md) to confirm recovery keys are available

## Next steps

- [Manage Disk Encryption policy for Windows devices with Intune](encrypt-devices.md)
- [Monitor disk encryption](../protect/encryption-monitor.md)
- [Troubleshooting BitLocker policy](/troubleshoot/mem/intune/troubleshoot-bitlocker-policies)
- [Known issues for Enforcing BitLocker policies with Intune](/windows/security/information-protection/bitlocker/ts-bitlocker-intune-issues)
- [BitLocker deployment comparison chart](/windows/security/information-protection/bitlocker/bitlocker-deployment-comparison)