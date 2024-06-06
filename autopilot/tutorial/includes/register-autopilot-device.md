---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-deploy
ms.service: windows-client
ms.topic: include
ms.date: 04/24/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-register-device.md
pre-provisioning/hybrid-azure-ad-join-register-device.md
self-deploying/self-deploying-register-device.md
user-driven/azure-ad-join-register-device.md
user-driven/hybrid-azure-ad-join-register-device.md

Headings are driven by article context. -->

Before a device can use Autopilot, the device must be registered as an Autopilot device. Registering a device as an Autopilot device can be thought of as importing the device into Autopilot so that Autopilot service can be used on the device. Registering a device as an Autopilot device doesn't mean that the device has ever used the Autopilot service. It just makes the Autopilot service available to the device.

Also note that a device registered in Autopilot doesn't mean the device is enrolled in Intune. A device may be registered as an Autopilot device but may not exist in Intune. It's not until an Autopilot registered device goes through the Autopilot process for the first time that it becomes enrolled in Intune. After the Autopilot device undergoes the Autopilot process and enrolls in Intune, the Autopilot device appears as a device in both Microsoft Entra ID and Intune.

> [!TIP]
>
> For Configuration Manager admins, registering a device as an Autopilot device before undergoing the Autopilot process for the first time can be thought of as being similar to Unknown Computer support.

There are several methods to register a device as an Autopilot device in Intune:

- Manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

  - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot)
  - [PowerShell script](/mem/autopilot/add-devices#powershell)
  - [Diagnostics page hash export](/mem/autopilot/add-devices#diagnostics-page-hash-export)
  - [Desktop hash export](/mem/autopilot/add-devices#desktop-hash-export)

  These methods of obtaining the hardware hash of a device are well documented. The corresponding documentation can be viewed by selecting the appropriate link from the above list.

- Automatically registering device via:

  - An [OEM](/mem/autopilot/oem-registration), including [Microsoft Surface](/surface/surface-autopilot-registration-support) devices
  - A [partner](/mem/autopilot/partner-registration)

  Registering a device via an OEM or partner is also well documented. The corresponding documentation can be viewed by selecting the appropriate link from the above list.

For most organizations, using an OEM or partner to register devices as Autopilot devices is the preferred, most common, and most secure method. However for smaller organizations, for testing/lab scenarios, and for emergency scenarios, manually registering devices as Autopilot devices via the hardware hash is also used.

> [!IMPORTANT]
>
> - Assuming that a device isn't currently enrolled Intune, remember that registering a device in Autopilot doesn't make it an Intune enrolled device. That device doesn't enroll into Intune until Autopilot runs on the device for the first time.
>
> - The following device shouldn't be registered as a Windows Autopilot device:
>
>   - [Microsoft Entra registered](/entra/identity/devices/concept-device-registration) devices, also known as "workplace joined" devices. For more information, see [Device appears as Microsoft Entra registered instead of Microsoft Entra joined](../../troubleshoot-device-enrollment.md#device-appears-as-microsoft-entra-registered-instead-of-microsoft-entra-joined).
>   - [Intune MDM-only enrollment](/mem/intune/enrollment/windows-enrollment-methods#user-self-enrollment-in-intune) devices.
>
>   These options are intended for users to join personally-owned devices to their organization's network. Windows Autopilot registered devices are registered as corporate owned devices.
>
>   If a device is already one of these two type of devices and it needs to be registered as a Windows Autopilot corporate device, it needs to first be removed from Microsoft Intune and Microsoft Entra ID before it's registered as a Windows Autopilot device. For more information, see [Deregister a device](../../registration-overview.md#deregister-a-device).

## Importing the hardware hash CSV file for devices into Intune

[!INCLUDE [Importing the hardware hash CSV file for devices into Intune](import-hardware-hash.md)]
