---
ms.topic: include
ms.date: 03/25/2025
---

<!-- This file is shared by the following articles:

/tutorial/includes/register-autopilot-device.md
registration-overview.md

Headings are driven by article context. -->

> [!IMPORTANT]
>
> The following type of devices shouldn't be registered as a Windows Autopilot device:
>
> - [Microsoft Entra registered](/entra/identity/devices/concept-device-registration) devices, also known as "workplace joined" devices.
> - [Intune MDM-only enrollment](/mem/intune-service/fundamentals/deployment-guide-enroll?tabs=byod-enrollment#windows-enrollment-methods) devices.
>
> These options are intended for users to join personally owned devices to their organization's network. Windows Autopilot registered devices are registered as corporate owned devices.
>
> If a device is already one of these two types of devices, to register is as a Windows Autopilot device, first remove it from Microsoft Intune and Microsoft Entra ID. For more information, see [Why is the join type for a device showing as "Microsoft Entra registered" instead of "Microsoft Entra joined"?](../troubleshooting-faq.yml#why-is-the-join-type-for-a-device-showing-as--microsoft-entra-registered--instead-of--microsoft-entra-joined--) and [Deregister a device](../registration-overview.md#deregister-a-device).
