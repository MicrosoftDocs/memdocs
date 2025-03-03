---
title: DFCI Management
description: With Windows Autopilot Deployment and Intune, Unified Extensible Firmware Interface (UEFI) settings can be managed after the device is enrolled. UEFI settings can be managed by using the Device Firmware Configuration Interface (DFCI).
ms.subservice: autopilot
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/27/2025
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: article
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Device Firmware Configuration Interface (DFCI) Management

With Windows Autopilot Deployment and Intune, Unified Extensible Firmware Interface (UEFI) settings can be managed after the device is enrolled. UEFI settings can be managed by using the Device Firmware Configuration Interface (DFCI). DFCI [enables Windows to pass management commands](/windows/client-management/mdm/uefi-csp) from Intune to UEFI for Autopilot deployed devices. This capability allows limiting end user's control over BIOS settings. For example, the boot options can be locked down to prevent users from booting up another OS, such as one that doesn't have the same security features.

If a user reinstalls a previous Windows version, installs a separate OS, or formats the hard drive, they can't override DFCI management. This feature can also prevent malware from communicating with OS processes, including elevated OS processes. DFCI's trust chain uses public key cryptography, and doesn't depend on local UEFI password security. This layer of security blocks local users from accessing managed settings from the device's UEFI menus.

For an overview of DFCI benefits, scenarios, and requirements, see [Device Firmware Configuration Interface (DFCI) Introduction](https://microsoft.github.io/mu/dyn/mu_feature_dfci/DfciPkg/Docs/Dfci_Feature/).

> [!IMPORTANT]
>
> A device automatically enrolls in DFCI management during Autopilot provisioning when the following actions occur:
>
> - The OEM enables the device for DFCI.
> - The device is registered for Autopilot via the OEM or a Cloud Solution Partner (CSP) in Partner Center.
>
> Enrollment in DFCI management triggers an additional reboot during the out-of-box experience (OOBE).

## DFCI management lifecycle

The DFCI management lifecycle includes the following processes:

- UEFI integration.
- Device registration.
- Profile creation.
- Enrollment.
- Management.
- Retirement.
- Recovery.

See the following figure:

:::image type="content" source="images/dfci.png" alt-text="Screenshot that shows Device Firmware Configuration Interface (DFCI) Management workflow":::

## Requirements

- A currently supported version of Windows and a supported UEFI is required.
- The device manufacturer must have DFCI added to their UEFI firmware in the manufacturing process, or as a firmware update that can be installed. Work with the device vendors to determine the [manufacturers that support DFCI](#oems-that-support-dfci), or the firmware version needed to use DFCI.
- The device must be managed with Microsoft Intune. For more information, see [Enroll Windows devices in Intune using Windows Autopilot](/mem/intune-service/enrollment/enrollment-autopilot).
- The device must be registered for Windows Autopilot by a [Microsoft Cloud Solution Provider (CSP) partner](https://partner.microsoft.com/membership/cloud-solution-provider), or registered directly by the OEM. For Surface devices, Microsoft registration support is available at [Microsoft Devices Autopilot Support](https://support.microsoft.com/supportrequestform/0d8bf192-cab7-6d39-143d-5a17840b9f5f).

> [!IMPORTANT]
>
> Devices manually registered for Autopilot (such as by [importing from a CSV file](/mem/intune-service/enrollment/enrollment-autopilot#add-devices)) aren't allowed to use DFCI. By design, DFCI management requires external attestation of the device's commercial acquisition through an OEM or a Microsoft CSP partner registration to Windows Autopilot. When the device is registered, its serial number is displayed in the list of Windows Autopilot devices.

## Managing DFCI profile with Windows Autopilot

There are four basic steps in managing DFCI profile with Windows Autopilot:

1. Create an Autopilot Profile
1. Create an Enrollment status page profile
1. Create a DFCI profile
1. Assign the profiles

See [Create the profiles](/mem/intune-service/configuration/device-firmware-configuration-interface-windows#create-the-profiles) and [Assign the profiles, and reboot](/mem/intune-service/configuration/device-firmware-configuration-interface-windows#assign-the-profiles-and-reboot) for details.

The existing [DFCI settings](/mem/intune-service/configuration/device-firmware-configuration-interface-windows#update-existing-dfci-settings) can also be changed on devices that are in use. In the existing DFCI profile, change the settings and save the changes. Since the profile is already assigned, the new DFCI settings take effect when next time the device syncs or the device reboots.

To identify whether a device is DFCI ready, the following Intune Graph API call can be used:

`managedDevice/deviceFirmwareConfigurationInterfaceManaged`

For more information, see [Intune devices and apps API overview](/graph/intune-concept-overview) and [Working with Intune in Microsoft Graph ](/graph/api/resources/intune-graph-overview).

## OEMs that support DFCI

- Acer.
- Asus.
- Dynabook.
- Fujitsu.
- [Microsoft Surface](/surface/surface-manage-dfci-guide).
- Panasonic.
- VAIO.
- Samsung.

Other OEMs are pending.

## Known issues

### DFCI enrollment fails for Professional editions of Windows 11, version 24H2

Date added: *October 9, 2024*
Date updated: *February 11, 2025*

DFCI can't currently be configured during the out-of-box experience (OOBE) on devices with Professional editions of Windows 11, version 24H2

For devices that have already been provisioned and have Professional editions of Windows 11, version 24H2, install [KB5046740](https://support.microsoft.com/topic/november-21-2024-kb5046740-os-build-26100-2454-preview-2040f716-b719-482a-8aff-f7f02c79b147) or later to enroll in DFCI. Devices with Professional editions of Windows 11, version 24H2 that have KB5046740 or later installed are automatically enrolled in DFCI after a reboot.

If DFCI needs to be configured during OOBE provisioning on 24H2 devices, follow these steps:

1. During OOBE onboarding, ensure the device is upgraded to the Enterprise edition of Windows 11, version 24H2.
1. After upgrading to the Enterprise edition of Windows 11, version 24H2, sync the device.
1. Once the device is synced, reboot it to get it enrolled in DFCI.

## Related content

- [Microsoft DFCI Scenarios](https://microsoft.github.io/mu/dyn/mu_feature_dfci/DfciPkg/Docs/Scenarios/DfciScenarios/).
- [Windows Autopilot and Surface devices](/surface/windows-autopilot-and-surface-devices).
