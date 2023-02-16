---
# required metadata

title: Device firmware configuration interface settings for Windows 10/11 in Microsoft Intune
description: See a list of all the DFCI profile settings and their descriptions on Windows 10/11 client devices. Use these settings in a configuration profile to control UEFI firmware layer features using Microsoft Intune policy. You can manage the CPU, built-in hardware, and boot options on Windows 10/11 client devices using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/19/2022
ms.topic: reference
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
- tier1
- M365-identity-device-management
- highpri
---

# Device Firmware Configuration Interface (DFCI) profile settings in Microsoft Intune

This article lists and describes the DFCI profile settings you can control on Windows client devices. As part of your mobile device management (MDM) solution, use these settings to control security features, the built-in hardware, and the boot options in the UEFI layer on Windows.

These settings apply to:

- Windows 11 on supported UEFI
- Windows 10 RS5 (1809) and later on supported UEFI

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your Windows client devices.

## Before you begin

- [Create the Windows 10/11 DFCI profile](device-firmware-configuration-interface-windows.md). There are more requirements to creating DFCI profiles. For more specific information, go to [Use DFCI profiles on Windows devices in Microsoft Intune](device-firmware-configuration-interface-windows.md).
- Some settings aren't available for all devices. To confirm if a setting is or isn't available on your device, contact your device manufacturer.
- These settings use the [UEFI CSP](/windows/client-management/mdm/uefi-csp).

> [!WARNING]
> Be careful. Configuring and assigning DFCI profiles can lock the device beyond repair. The DFCI profile settings change the device hardware, and can't be fixed by re-imaging the OS.

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

## Cameras

- **Cameras**: This setting manages all the hardware cameras built into the device. It doesn't manage attached peripherals, such as USB webcams.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in cameras.
  - **Enabled**: All built-in cameras directly managed by UEFI (BIOS) are enabled. Peripherals, like USB cameras, aren't affected.
  - **Disabled**: All built-in cameras directly managed by UEFI (BIOS) are disabled. Peripherals, like USB cameras, aren't affected.

- **Front cameras**: This setting manages the built-in front visible light cameras managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in front visible light cameras.
  - **Enabled**: All built-in front visible light cameras directly managed by UEFI (BIOS) are enabled. Peripherals, like USB cameras, aren't affected.
  - **Disabled**: All built-in front visible light cameras directly managed by UEFI (BIOS) are disabled. Peripherals, like USB cameras, aren't affected.

- **Rear cameras**: This setting manages the built-in rear visible light cameras managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in rear cameras.
  - **Enabled**: All built-in rear visible light cameras directly managed by UEFI (BIOS) are enabled. Peripherals, like USB cameras, aren't affected.
  - **Disabled**: All built-in rear visible light cameras directly managed by UEFI (BIOS) are disabled. Peripherals, like USB cameras, aren't affected.

- **Infrared (IR) cameras**: This setting manages the built-in infrared cameras managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in infrared cameras.
  - **Enabled**: All built-in infrared cameras directly managed by UEFI (BIOS) are enabled. Peripherals, like USB cameras, aren't affected.
  - **Disabled**: All built-in infrared cameras directly managed by UEFI (BIOS) are disabled. Peripherals, like USB cameras, aren't affected.

## Microphones and speakers

> [!TIP]
> Configure the category setting (**Microphones and speakers**) **or** the granular settings (**Microphones**). If you configure all the settings, these settings can cause a conflict. For more information, go to [DFCI profile overview: Conflicts](device-firmware-configuration-interface-windows.md#conflicts).

- **Microphones and speakers**: This setting manages all the microphones and speakers built into the device. It doesn't manage attached peripherals, such as USB devices.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in microphones and speakers.
  - **Enabled**: All built-in microphones and speakers directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in microphones and speakers directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

- **Microphones**: This setting manages the built-in microphones managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in microphones.
  - **Enabled**: All built-in microphones directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in microphones directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

## Radios

> [!TIP]
> Configure the category setting (**Radios (Bluetooth, Wi-Fi, NFC, etc.)**) **or** the granular settings (**Bluetooth**, **Wi-Fi**). If you configure all the settings, these settings can cause a conflict. For more information, go to [DFCI profile overview: Conflicts](device-firmware-configuration-interface-windows.md#conflicts).

- **Radios (Bluetooth, Wi-Fi, NFC, etc.)**: This setting manages all the built-in radios managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable all built-in radios.
  - **Enabled**: All built-in radios directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in radios directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

    > [!WARNING]
    > If you disable the **Radios** setting, the device requires a wired network connection. Otherwise, the device may be unmanageable.

- **Bluetooth**: This setting manages the built-in Bluetooth radios managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in Bluetooth radios.
  - **Enabled**: All built-in Bluetooth radios directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in Bluetooth radios directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

- **WWAN**: This setting manages the built-in WWAN radios managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in WWAN radios.
  - **Enabled**: All built-in WWAN radios directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in WWAN radios directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

- **NFC**: This setting manages the built-in NFC radios managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in NFC radios.
  - **Enabled**: All built-in NFC radios directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in NFC radios directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

- **Wi-Fi**: This setting manages the built-in Wi-Fi radios managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in Wi-Fi radios.
  - **Enabled**: All built-in Wi-Fi radios directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in Wi-Fi radios directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

## Boot Options

> [!WARNING]
> Disabling all external boot options or all external ports significantly complicates OS recovery. To recover a device that can no longer boot Windows, you may have to physically open the device and replace the hardware storage.

- **Boot from external media (USB, SD)**: Your options:
  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might allow booting from external media.
  - **Enabled**: UEFI (BIOS) allows booting from non-hard drive storage.
  - **Disabled**: UEFI (BIOS) prevents booting from non-hard drive storage, which also disables booting from network adapters.

    When set to **Disabled**, don't set the **Boot from network adapters** setting to **Enabled**. It causes the **Boot from external media (USB, SD)** setting or **Boot from network adapters** setting to become not compliant.

- **Boot from network adapters**: Your options:
  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might allow booting from built-in network adapters.
  - **Enabled**: UEFI (BIOS) allows booting from built-in network interfaces.
  - **Disabled**: UEFI (BIOS) prevents booting built-in network interfaces.

## Ports

> [!WARNING]
> Disabling all external boot options or all external ports significantly complicates OS recovery. To recover a device that can no longer boot Windows, you may have to physically open the device and replace the hardware storage.

- **USB type A**: This setting manages the built-in USB type A ports managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in USB type A ports.
  - **Enabled**: All built-in USB type A ports directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in USB type A ports directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

- **SD card**: This setting manages the built-in SD card ports managed by UEFI (BIOS). It doesn't manage attached peripherals.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable the built-in SD card ports.
  - **Enabled**: All built-in SD card ports directly managed by UEFI (BIOS) are enabled. Peripherals, like USB devices, aren't affected.
  - **Disabled**: All built-in SD card ports directly managed by UEFI (BIOS) are disabled. Peripherals, like USB devices, aren't affected.

## Wake settings

> [!WARNING]
> Disabling all external boot options or all external ports significantly complicates OS recovery. To recover a device that can no longer boot Windows, you may have to physically open the device and replace the hardware storage.

- **Wake on LAN**: Wake on LAN allows a network administrator to remotely wake a device in sleep mode using the LAN.

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might prevent waking a device using the LAN.
  - **Enabled**: UEFI (BIOS) allows waking a device using the LAN.
  - **Disabled**: UEFI (BIOS) prevents waking a device using the LAN.

- **Wake on power**: Wake on power allows a network administrator to remotely wake a device in sleep mode when it's connected to a power source. Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might prevent waking a device when it's connected to a power source.
  - **Enabled**: UEFI (BIOS) allows waking a device when it's connected to a power source.
  - **Disabled**: UEFI (BIOS) prevents waking a device when it's connected to a power source.

## Next steps

For other technical details on each setting and what editions of Windows are supported, see [Windows 10/11 Policy CSP Reference](/windows/client-management/mdm/policy-configuration-service-provider).

[Use DFCI profiles on Windows devices in Microsoft Intune](device-firmware-configuration-interface-windows.md).

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
