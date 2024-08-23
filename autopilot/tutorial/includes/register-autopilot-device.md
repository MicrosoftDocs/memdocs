---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-register-device.md
pre-provisioning/hybrid-azure-ad-join-register-device.md
self-deploying/self-deploying-register-device.md
user-driven/azure-ad-join-register-device.md
user-driven/hybrid-azure-ad-join-register-device.md

Headings are driven by article context. -->

Before a device can use Autopilot, the device must be registered as an Autopilot device. Registering a device as an Autopilot device can be thought of as importing the device into Autopilot so that Autopilot service can be used on the device. Registering a device as an Autopilot device doesn't mean that the device has used the Autopilot service. It just makes the Autopilot service available to the device.

Also note that a device registered in Autopilot doesn't mean the device is enrolled in Intune. A device might be registered as an Autopilot device but might not exist in Intune. It's not until an Autopilot registered device goes through the Autopilot process for the first time that it becomes enrolled in Intune. After the Autopilot device undergoes the Autopilot process and enrolls in Intune, the Autopilot device appears as a device in both Microsoft Entra ID and Intune.

There are several methods to register a device as an Autopilot device in Intune:

- Manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

  - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot).
  - [PowerShell script](../../add-devices.md#powershell).
  - [Diagnostics page hash export](../../add-devices.md#diagnostics-page-hash-export).
  - [Desktop hash export](../../add-devices.md#desktop-hash-export).

  These methods of obtaining the hardware hash of a device are well documented. The corresponding documentation can be viewed by selecting the appropriate link from the above list.

- Automatically registering device via:

  - An [OEM](../../oem-registration.md), including [Microsoft Surface](/surface/surface-autopilot-registration-support) devices.
  - A [partner](../../partner-registration.md).

  Registering a device via an OEM or partner is also well documented. The corresponding documentation can be viewed by selecting the appropriate link from the above list.

For most organizations, using an OEM or partner to register devices as Autopilot devices is the preferred, most common, and most secure method. However for smaller organizations, for testing/lab scenarios, and for emergency scenarios, manually registering devices as Autopilot devices via the hardware hash is also used.

[!INCLUDE [Registered device warning](../../includes/registered-vs-joined.md)]

> [!NOTE]
>
> Assuming that a device isn't currently enrolled Intune, remember that registering a device in Autopilot doesn't make it an Intune enrolled device. That device doesn't enroll into Intune until Autopilot runs on the device for the first time.

## Importing the hardware hash CSV file for devices into Intune

[!INCLUDE [Importing the hardware hash CSV file for devices into Intune](import-hardware-hash.md)]
