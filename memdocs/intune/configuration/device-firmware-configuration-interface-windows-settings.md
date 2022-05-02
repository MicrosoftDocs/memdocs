---
# required metadata

title: Device firmware configuration interface settings for Windows 10/11 in Microsoft Intune
description: See a list of all the DFCI profile settings and their descriptions on Windows 10/11 client devices. Use these settings in a configuration profile to control UEFI firmware layer features using Microsoft Intune policy. You can manage the CPU, built-in hardware, and boot options on Windows 10/11 client devices using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/02/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; 
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Device Firmware Configuration Interface (DFCI) profile settings in Microsoft Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article lists and describes the DFCI profile settings you can control on Windows client devices. As part of your mobile device management (MDM) solution, use these settings to control security features, the built-in hardware, and the boot options in the UEFI layer on Windows.

These settings apply to:

- Windows 11 on supported UEFI
- Windows 10 RS5 (1809) and later on supported UEFI

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your Windows client devices.

## Before you begin

- [Create the Windows 10/11 DFCI profile](device-firmware-configuration-interface-windows.md). There are more requirements to creating DFCI profiles. For more specific information, go to [Use DFCI profiles on Windows devices in Microsoft Intune](device-firmware-configuration-interface-windows.md).
- These settings use the [UEFI CSP](/windows/client-management/mdm/uefi-csp).

## Security features

- **Allow local user to change UEFI settings**: Your options:
  - **Only not configured settings**: The local user can change any setting *except* those settings explicitly set to **Enable** or **Disable** by Intune.
  - **None**: The local user may not change any UEFI (BIOS) settings, including settings not shown in the DFCI profile.

- **CPU and IO virtualization**: Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **Enabled**: The BIOS enables the platform's CPU and IO virtualization capabilities for use by the OS. It turns on Windows Virtualization Based Security and Device Guard technologies.

- **Windows Platform Binary Table** (WPBT): The WPBT allows vendors and OEMs to run an `.exe` program in the UEFI layer. Every time Windows boots, it looks at the UEFI, and runs the `.exe`. It's used to run programs that aren't included with the Windows media.

  Your options:
  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might allow vendors and OEMs to run programs using the WPBT.
  - **Enabled**: Enables the WPBT and allows `.exe` programs in the UEFI layer to run.
  - **Disabled**: Disables the WPBT and prevents `.exe` programs in the UEFI layer from running.

- **Simultaneous multithreading** (SMT): Also known as hyper-threading. Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **Enabled**: Enables SMT in the UEFI layer.
  - **Disabled**: Disables SMT in the UEFI layer.

## Built-in Hardware

These settings manage the hardware components built into the devices. They don't manage attached peripherals, such as USB webcams.

- **Cameras**: Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **Enabled**: All built-in cameras directly managed by UEFI (BIOS) are enabled. Peripherals, like USB cameras, aren't affected.
  - **Disabled**: All built-in camera directly managed by UEFI (BIOS) are disabled. Peripherals, like USB cameras, aren't affected.

- **Microphones and speakers**:  Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **Enabled**: All built-in microphones and speakers directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in microphones and speakers directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

- **Radios (Bluetooth, Wi-Fi, NFC, etc.)**: Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **Enabled**: All built-in radios directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in radios directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

    > [!WARNING]
    > If you disable the **Radios** setting, the device requires a wired network connection. Otherwise, the device may be unmanageable.

## Boot Options

- **Boot from external media (USB, SD)**: Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **Enabled**: UEFI (BIOS) allows booting from non-hard drive storage.
  - **Disabled**: UEFI (BIOS) doesn't allow booting from non-hard drive storage, which also disables booting from network adapters. 

    When set to **Disabled**, don't set the **Boot from network adapters** setting to **Enabled**. It causes the **Boot from external media (USB, SD)** setting or **Boot from network adapters** setting to become not compliant.

- **Boot from network adapters**: Your options:
  - **Not configured**: Intune doesn't change or update this setting.
  - **Enabled**: UEFI (BIOS) allows booting from built-in network interfaces.
  - **Disabled**: UEFI (BIOS) doesn't allow booting built-in network interfaces.

## Next steps

For other technical details on each setting and what editions of Windows are supported, see [Windows 10/11 Policy CSP Reference](/windows/client-management/mdm/policy-configuration-service-provider)

[Use DFCI profiles on Windows devices in Microsoft Intune](device-firmware-configuration-interface-windows.md).

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
