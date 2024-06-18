---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-deploy
ms.service: windows-client
ms.topic: include
ms.date: 06/07/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

/tutorial/includes/register-autopilot-device.md
registration-overview.md

Headings are driven by article context. -->

> [!IMPORTANT]
>
> The following device shouldn't be registered as a Windows Autopilot device:
>
> - [Microsoft Entra registered](/entra/identity/devices/concept-device-registration) devices, also known as "workplace joined" devices.
> - [Intune MDM-only enrollment](/mem/intune/enrollment/windows-enrollment-methods#user-self-enrollment-in-intune) devices.
>
> These options are intended for users to join personally-owned devices to their organization's network. Windows Autopilot registered devices are registered as corporate owned devices.
>
> If a device is already one of these two type of devices and it needs to be registered as a Windows Autopilot corporate device, it needs to first be removed from Microsoft Intune and Microsoft Entra ID before it's registered as a Windows Autopilot device. For more information, see [Device appears as Microsoft Entra registered instead of Microsoft Entra joined](../troubleshoot-device-enrollment.md#device-appears-as-microsoft-entra-registered-instead-of-microsoft-entra-joined) and [Deregister a device](../registration-overview.md#deregister-a-device).
