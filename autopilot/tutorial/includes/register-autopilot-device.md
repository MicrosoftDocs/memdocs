---
ms.topic: include
ms.date: 03/25/2025
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-register-device.md
pre-provisioning/hybrid-azure-ad-join-register-device.md
self-deploying/self-deploying-register-device.md
user-driven/azure-ad-join-register-device.md
user-driven/hybrid-azure-ad-join-register-device.md

Headings are driven by article context. -->

Before a device can use Windows Autopilot, the device must be registered as a Windows Autopilot device. Registering a device as a Windows Autopilot device can be thought of as importing the device into Windows Autopilot so that Windows Autopilot service can be used on the device. Registering a device as a Windows Autopilot device doesn't mean that the device has used the Windows Autopilot service. It just makes the Windows Autopilot service available to the device.

Also note that a device registered in Windows Autopilot doesn't mean the device is enrolled in Intune. A device might be registered as a Windows Autopilot device but might not exist in Intune. It's not until a Windows Autopilot registered device goes through the Windows Autopilot process for the first time that it becomes enrolled in Intune. After the Windows Autopilot device undergoes the Windows Autopilot process and enrolls in Intune, the Windows Autopilot device appears as a device in both Microsoft Entra ID and Intune.

There are several methods to register a device as a Windows Autopilot device in Intune:

- Manually registering devices into Intune as a Windows Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

  - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot).
  - [PowerShell script](../../add-devices.md#powershell).
  - [Diagnostics page hash export](../../add-devices.md#diagnostics-page-hash-export).
  - [Desktop hash export](../../add-devices.md#desktop-hash-export).

  These methods of obtaining the hardware hash of a device are well documented. The corresponding documentation can be viewed by selecting the appropriate link from the above list.

- Automatically registering device via:

  - An [OEM](../../oem-registration.md), including [Microsoft Surface](/surface/surface-autopilot-registration-support) devices.
  - A [partner](../../partner-registration.md).

  Registering a device via an OEM or partner is also well documented. The corresponding documentation can be viewed by selecting the appropriate link from the above list.

For most organizations, using an OEM or partner to register devices as Windows Autopilot devices is the preferred, most common, and most secure method. However for smaller organizations, for testing/lab scenarios, and for emergency scenarios, manually registering devices as Windows Autopilot devices via the hardware hash is also used.

[!INCLUDE [Registered device warning](../../includes/registered-vs-joined.md)]

> [!NOTE]
>
> Assuming that a device isn't currently enrolled Intune, remember that registering a device in Windows Autopilot doesn't make it an Intune enrolled device. That device doesn't enroll into Intune until Windows Autopilot runs on the device for the first time.

## Importing the hardware hash CSV file for devices into Intune

[!INCLUDE [Importing the hardware hash CSV file for devices into Intune](import-hardware-hash.md)]
