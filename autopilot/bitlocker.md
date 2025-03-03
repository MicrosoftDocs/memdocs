---
title: Setting the BitLocker encryption algorithm for Autopilot devices
description: Microsoft Intune provides a comprehensive set of configuration options to manage BitLocker on Windows devices.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: how-to
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Setting the BitLocker encryption algorithm for Autopilot devices

BitLocker [automatically encrypts](/windows-hardware/design/device-experiences/oem-bitlocker#bitlocker-automatic-device-encryption) internal drives during the out-of-box experience (OOBE) for devices that support [Modern Standby](/windows-hardware/design/device-experiences/modern-standby) or meet the [Hardware Security Testability Specification (HSTI)](/windows-hardware/test/hlk/testref/hardware-security-testability-specification). By default, BitLocker uses XTS-AES 128-bit used space only for automatic encryption.

With Windows Autopilot, BitLocker encryption settings can be configured to apply before automatic encryption starts. This configuration makes sure the default encryption algorithm or type isn't applied automatically. A device that receives these settings after encrypting automatically needs to be decrypted before changing the encryption algorithm.

## Encryption algorithm

BitLocker uses the specified BitLocker encryption algorithm when BitLocker is first enabled. During Autopilot, BitLocker will be enabled after the device setup portion of the [enrollment status page](enrollment-status.md). The following encryption algorithms are available:

- AES-CBC 128-bit.
- AES-CBC 256-bit.
- XTS-AES 128-bit (default).
- XTS-AES 256-bit.

For more information about the recommended encryption algorithms to use, see [BitLocker Configuration Service Provider (CSP)](/windows/client-management/mdm/bitlocker-csp).

To make sure the desired BitLocker encryption algorithm is set before automatic encryption occurs for Autopilot devices:

1. Configure the [encryption method settings](/mem/intune-service/protect/encrypt-devices#create-an-endpoint-security-policy-for-bitlocker) in the Endpoint Security disk encryption policy. The settings are available under **Endpoint Security** > **Disk encryption** > **Create policy** > **Platform** = Windows 10 and later, **Profile type** = BitLocker.

1. [Assign the policy](/mem/intune-service/configuration/device-profile-assign) to the Autopilot device group. The encryption policy must be assigned to **devices** in the group, not users.

1. Enable the Autopilot [enrollment status page](enrollment-status.md) for these devices. If this feature isn't enabled, the policy doesn't apply before encryption starts.

## Full disk or used space-only encryption

There are two types of encryption, full disk or used space-only. Configuration of [silent enablement](/mem/intune-service/protect/encrypt-devices#silently-enable-bitlocker-on-devices) and hardware support for modern standby automatically determines the type of encryption used. The type of encryption used can be enforced by configuring the [SystemDrivesEncryptionType](/windows/client-management/mdm/bitlocker-csp) setting. Like the encryption algorithm, BitLocker uses the encryption type when BitLocker is first enabled. For more information on the expected encryption type behavior, see [Manage BitLocker policy](/mem/intune-service/protect/encrypt-devices#full-disk-vs-used-space-only-encryption).

To enforce the type of drive encryption used:

1. Configure the **Enforce drive encryption type on operating system drives** setting within the [settings catalog](/mem/intune-service/configuration/settings-catalog). This setting is available in the **Administrative Templates > Windows Components > BitLocker Drive Encryption > Operating System Drives** category from the settings picker.

1. [Assign the policy](/mem/intune-service/configuration/device-profile-assign) to the Autopilot device group. The encryption policy must be assigned to **devices** in the group, not users.

1. Enable the Autopilot [enrollment status page](enrollment-status.md) for these devices. If this feature isn't enabled, the policy doesn't apply before encryption starts.

## Related content

- [BitLocker overview](/windows/security/information-protection/bitlocker/bitlocker-overview).
- [Manage BitLocker policy for Windows devices with Intune](/mem/intune-service/protect/encrypt-devices).
