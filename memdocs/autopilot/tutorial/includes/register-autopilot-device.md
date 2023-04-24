---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
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

Also note that a device registered in Autopilot doesn't mean the device is enrolled in Intune. A device may be registered as an Autopilot device but may not exist in Intune. It's not until an Autopilot registered device goes through the Autopilot process for the first time that it becomes enrolled in Intune. After the Autopilot device undergoes the Autopilot process and enrolls in Intune, the Autopilot device subsequently appears as a device in both Azure AD and Intune.

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
> Assuming that a device isn't currently enrolled Intune, remember that registering a device in Autopilot doesn't make it an Intune enrolled device. That device won't enroll into Intune until Autopilot runs on the device for the first time.

## Importing the hardware hash CSV file for devices into Intune

[!INCLUDE [Importing the hardware hash CSV file for devices into Intune](import-hardware-hash.md)]
