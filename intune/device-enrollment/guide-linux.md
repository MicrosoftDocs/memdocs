---
title: Linux device enrollment guide for Microsoft Intune
description: Enroll Linux devices in Intune using the Intune app. Set an overview of the administrator and end user tasks to enroll devices.
author: MandiOhlinger
ms.author: mandia
ms.date: 03/31/2026
ms.topic: article
ms.reviewer: arnab
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---


# Enrollment guide: Enroll Linux desktop devices in Microsoft Intune

Linux devices can be enrolled in Intune. Once they're enrolled, they receive the policies you create. Users can use the Microsoft Edge browser to access organization resources.

This article includes an overview of the administrator and user tasks required to enroll Linux devices.

## Before you begin

For all Intune-specific prerequisites and configurations needed to prepare your tenant for enrollment, go to [Enrollment guide: Microsoft Intune enrollment](guide.md).

## Linux enrollment

Use for personal/BYOD and organization-owned devices running Linux.

---
| Feature | Use this enrollment option when |
| --- | --- |
| You use Ubuntu Desktop (24.04 LTS or 22.04 LTS on x86/64). | ✅ |
| You use Ubuntu Server. | ❌ |
| You use RedHat Enterprise Linux 9 or 10. |✅ |
| Devices are owned by the organization or school. | ✅ |
| Devices are personal or BYOD. | ✅  |
| You have new or existing devices. | ✅ |
| Need to enroll a few devices, or a large number of devices (bulk enrollment). | ❌ <br/><br/> Bulk enrollment isn't supported. Each device needs to be enrolled using the Microsoft Intune App. |
| Devices are associated with a single user. | ✅ |
| Devices are user-less, such as kiosk or dedicated device. | ❌ <br/><br/> The enrollment requires a user to sign in with an organization account. |
| Devices are managed by another MDM provider. | ❌ <br/><br/> It might be possible to enroll Linux devices in Intune that are already enrolled in another MDM provider. This scenario hasn't been tested by Microsoft. |
| You use the device enrollment manager (DEM) account. | ❌ <br/><br/> DEM accounts don't apply to Linux. |

---

## Administrator tasks

Other than having Intune setup, there are minimal administrator tasks with Linux enrollment.

- Be sure your devices are [supported](../intune-service/fundamentals/supported-devices-browsers.md).
- Intune admins don't do anything to enable Linux enrollment in the Microsoft Intune admin center. It's automatically enabled. When users enroll their Linux devices, you see them in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **By platform** > **Linux**.  
- Versions 2.0.2 and later of the Microsoft Identity Broker included with the Microsoft Intune app for Linux introduce a major architectural change from the previous Java‑based broker. When Linux devices update from earlier broker versions, Intune automatically re‑registers and re‑enrolls the devices and creates new Intune device IDs and Microsoft Entra device IDs for them. This behavior requires no user action, but we recommend that admins review device‑based assignments, filters, and Microsoft Entra ID group memberships that rely on device IDs to ensure that policies apply correctly.  

## End user tasks

The following steps provide an overview. For the specific steps, go to [Enroll a Linux device in Intune](../user-help/enrollment/enroll-linux.md).

> [!TIP]
> When end users install the OS, it's recommended to enable encryption on the hard disk. After the OS is installed, it can be difficult to enable encryption.

1. [Download and install Microsoft Edge browser](https://www.microsoft.com/edge) version 102.x and newer.
2. [Download and install the Microsoft Intune app for Linux](../user-help/company-portal/intune-app-linux.md). The install can take several minutes and requires a reboot. This app registers the device with Intune.
3. Users open the Intune app, and sign in with their organization account (`user@contoso.com`). After they sign in, the enrollment process starts. It's possible users might be prompted to configure other settings based on your compliance policies.
4. Users open Microsoft Edge and sign in with their organization account (`user@contoso.com`). After they sign in, they can access your organization's resources, like internal websites and Microsoft 365 apps.

## Related articles  

For more information about Linux device management, see:  
- [Microsoft single sign-on for Linux](/entra/identity/devices/sso-linux)
- [Troubleshoot device registration command tool](/entra/identity/devices/troubleshoot-device-registration-tool-linux?tabs=debian-dsreginstall)  

For more device enrollment guides, see:  

- [MAM](../intune-service/fundamentals/deployment-guide-enrollment-mamwe.md)
- [Android enrollment guide](android/guide.md)
- [iOS/iPadOS enrollment guide](apple/guide-ios-ipados.md)
- [macOS enrollment guide](apple/guide-macos.md)
- [Windows enrollment guide](windows/guide.md)
