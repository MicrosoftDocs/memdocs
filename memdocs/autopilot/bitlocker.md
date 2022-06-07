---
title: Setting the BitLocker encryption algorithm for Autopilot devices
description: Microsoft Intune provides a comprehensive set of configuration options to manage BitLocker on Windows devices. 
keywords: Autopilot, BitLocker, encryption, 256-bit, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: how-to
---


# Setting the BitLocker encryption algorithm for Autopilot devices

**Applies to**

- Windows 11
- Windows 10

BitLocker [automatically encrypts](/windows-hardware/design/device-experiences/oem-bitlocker#bitlocker-automatic-device-encryption) internal drives during the Out Of Box Experience (OOBE) for devices that support [Modern Standby](/windows-hardware/design/device-experiences/modern-standby) or meet the [Hardware Security Testability Specification (HSTI)](/windows-hardware/test/hlk/testref/hardware-security-testability-specification). By default, BitLocker uses XTS-AES 128-bit used space only for automatic encryption. 

With Windows Autopilot, you can configure BitLocker encryption settings to get applied before automatic encryption starts. This configuration makes sure the default encryption algorithm or type isn't applied automatically. A device that recieves these settings after encrypting automatically will need to be decrypted before changing the encryption algorithm.

## <span id="Encryption_algorithm"></span>Encryption algorithm

The BitLocker encryption algorithm is used when BitLocker is first enabled. During Autopilot, BitLocker will be enabled after the Device setup portion of the [Enrollment Status Page](enrollment-status.md) (ESP). Available encryption algorithms are: AES-CBC 128-bit, AES-CBC 256-bit, XTS-AES 128-bit, or XTS-AES 256-bit encryption. The default value is XTS-AES 128-bit encryption. See [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp) for information about the recommended encryption algorithms to use.

To make sure the BitLocker encryption algorithm you want is set before automatic encryption occurs for Autopilot devices:

1. Configure the [encryption method settings](../intune/protect/encrypt-devices#create-an-endpoint-security-policy-for-bitlocker) in the Endpoint Security disk encryption policy. The settings are available under **Endpoint Security** > **Disk encryption** > **Create policy** > **Platform** = Windows 10 and later, **Profile type** = BitLocker. 
2. [Assign the policy](../intune/configuration/device-profile-assign.md) to your Autopilot device group. The encryption policy must be assigned to **devices** in the group, not users.
3. Enable the Autopilot [Enrollment Status Page](enrollment-status.md) (ESP) for these devices. If the ESP isn't enabled, the policy won't apply before encryption starts.

An example of Endpoint Security disk encryption settings is shown below.

![BitLocker Endpoint Security disk encryption profile.](https://user-images.githubusercontent.com/43853653/172425590-fec5d23f-b7ae-47a0-a921-427756cbbe46.png)

## <span id="Full_disk_vs_Used_Space_only_encryption"></span>Full disk vs Used Space only encryption

The type of drive encryption (full disk or used space only) is automatically determined by configuration of [silent enablement](/mem/intune/protect/encrypt-devices#silently-enable-bitlocker-on-devices) and hardware support for modern standby, but can be enforced by configuring the [SystemDrivesEncryptionType](/windows/client-management/mdm/bitlocker-csp) setting. Like the encryption algorithm, the encryption type is used when BitLocker is first enabled.  See [Manage BitLocker policy](/mem/intune/protect/encrypt-devices#full-disk-vs-used-space-only-encryption) for information on expected encryption type behavior.

To enforce the type of drive encryption used:

1. Configure the 'Enforce drive encryption type on operating system drives' setting within the [settings catalog](/mem/intune/configuration/settings-catalog). This setting is available in the **Administrative Templates > Windows Components > BitLocker Drive Encryption > Operating System Drives** category from the settings picker. 
2. [Assign the policy](../intune/configuration/device-profile-assign.md) to your Autopilot device group. The encryption policy must be assigned to **devices** in the group, not users.
3. Enable the Autopilot [Enrollment Status Page](enrollment-status.md) (ESP) for these devices. If the ESP isn't enabled, the policy won't apply before encryption starts.

An example of the settings catalog profile is shown below.

![BitLocker settings catalog drive type](https://user-images.githubusercontent.com/43853653/172427108-bf3803e9-fd50-4663-85cc-83135b7a4f4f.png)


## Requirements

Windows 10, version 1809 or later.

## Next steps

[BitLocker overview](/windows/security/information-protection/bitlocker/bitlocker-overview)
[Manage BitLocker policy for Windows devices with Intune](/mem/intune/protect/encrypt-devices)
