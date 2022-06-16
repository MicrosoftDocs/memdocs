---
title: Setting the BitLocker encryption algorithm for Autopilot devices
description: Microsoft Intune provides a comprehensive set of configuration options to manage BitLocker on Windows devices. 
ms.prod: w10
ms.localizationpriority: medium
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 06/15/2022
ms.collection: M365-modern-desktop
ms.topic: how-to
---

# Setting the BitLocker encryption algorithm for Autopilot devices

**Applies to**

- Windows 11
- Windows 10

BitLocker [automatically encrypts](/windows-hardware/design/device-experiences/oem-bitlocker#bitlocker-automatic-device-encryption) internal drives during the out of box experience (OOBE) for devices that support [Modern Standby](/windows-hardware/design/device-experiences/modern-standby) or meet the [Hardware Security Testability Specification (HSTI)](/windows-hardware/test/hlk/testref/hardware-security-testability-specification). By default, BitLocker uses XTS-AES 128-bit used space only for automatic encryption.

With Windows Autopilot, you can configure BitLocker encryption settings to apply before automatic encryption starts. This configuration makes sure the default encryption algorithm or type isn't applied automatically. A device that receives these settings after encrypting automatically will need to be decrypted before changing the encryption algorithm.

## Encryption algorithm

The BitLocker encryption algorithm is used when BitLocker is first enabled. During Autopilot, BitLocker will be enabled after the device setup portion of the [enrollment status page](enrollment-status.md). The following encryption algorithms are available:

- AES-CBC 128-bit
- AES-CBC 256-bit
- XTS-AES 128-bit (default)
- XTS-AES 256-bit

For more information about the recommended encryption algorithms to use, see [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp).

To make sure the BitLocker encryption algorithm you want is set before automatic encryption occurs for Autopilot devices:

1. Configure the [encryption method settings](../intune/protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker) in the Endpoint Security disk encryption policy. The settings are available under **Endpoint Security** > **Disk encryption** > **Create policy** > **Platform** = Windows 10 and later, **Profile type** = BitLocker.

2. [Assign the policy](../intune/configuration/device-profile-assign.md) to your Autopilot device group. The encryption policy must be assigned to **devices** in the group, not users.

3. Enable the Autopilot [enrollment status page](enrollment-status.md) for these devices. If you don't enable this feature, the policy won't apply before encryption starts.

The following image is an example of the Endpoint Security disk encryption settings.

:::image type="content" source="media/bitlocker/endpoint-security-disk-encryption-policy.png" alt-text="Screenshot example of the Endpoint Security disk encryption settings.":::

## Full disk or used space-only encryption

There are two types of encryption, full disk or used space-only. The type of encryption is automatically determined by configuration of [silent enablement](../intune/protect/encrypt-devices.md#silently-enable-bitlocker-on-devices) and hardware support for modern standby. You can enforce it by configuring the [SystemDrivesEncryptionType](/windows/client-management/mdm/bitlocker-csp) setting. Like the encryption algorithm, the encryption type is used when BitLocker is first enabled. For more information on the expected encryption type behavior, see [Manage BitLocker policy](../intune/protect/encrypt-devices.md#full-disk-vs-used-space-only-encryption).

To enforce the type of drive encryption used:

1. Configure the **Enforce drive encryption type on operating system drives** setting within the [settings catalog](../intune/configuration/settings-catalog.md). This setting is available in the **Administrative Templates > Windows Components > BitLocker Drive Encryption > Operating System Drives** category from the settings picker.

2. [Assign the policy](../intune/configuration/device-profile-assign.md) to your Autopilot device group. The encryption policy must be assigned to **devices** in the group, not users.

3. Enable the Autopilot [enrollment status page](enrollment-status.md) for these devices. If you don't enable this feature, the policy won't apply before encryption starts.

The following image is an example of the settings catalog profile.

:::image type="content" source="media/bitlocker/settings-catalog-drive-type.png" alt-text="Screenshot example of the BitLocker drive type configuration in the settings catalog.":::

## Requirements

A supported version of Windows 11 or Windows 10.

## Next steps

[BitLocker overview](/windows/security/information-protection/bitlocker/bitlocker-overview)

[Manage BitLocker policy for Windows devices with Intune](../intune/protect/encrypt-devices.md)
