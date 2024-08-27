---
title: Windows Autopilot registration overview
description: Overview of Windows Autopilot device registration.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: how-to
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Windows Autopilot registration overview

Before a device is deployed using Windows Autopilot, the device must be registered with the Windows Autopilot deployment service.

Successful registration requires that two processes are complete:

1. The device's unique [hardware identity](#device-identification) (known as a hardware hash) is captured and uploaded to the Autopilot service.
1. The device is associated to an Azure tenant ID.

Ideally, the OEM, reseller, or distributor performs both of these processes from which the devices were purchased. An OEM or other device provider uses the [registration authorization](registration-auth.md) process to perform device registration on behalf of the organization.

Registration can also be performed within the organization by collecting the hardware identity from new or existing devices and [uploading it manually](manual-registration.md). If devices meet certain requirements, they can also be configured for [automatic registration](automatic-registration.md) with Windows Autopilot. For more information about the ways in which devices can be registered with Windows Autopilot, see the following overview articles:

- [OEM registration](oem-registration.md)
- [Reseller, distributor, or partner registration](partner-registration.md)
- [Automatic registration](automatic-registration.md)
- [Manual registration](manual-registration.md)

When an Autopilot device is registered, it automatically creates a Microsoft Entra object. The Autopilot deployment process needs this object to identify the device before the user signs in. If the object is deleted, the device can fail to enroll through Autopilot.

[!INCLUDE [Registered device warning](includes/registered-vs-joined.md)]

If a profile isn't assigned to a Windows Autopilot device, it receives the default Windows Autopilot profile. If a device shouldn't go through Autopilot, remove the Windows Autopilot registration.

## Terms

The following terms are used to refer to various steps in the registration process:

| **Term** | **Definition** |
| --- | --- |
| **Device registration** | Device registration happens when a device's hardware hash is associated with the Windows Autopilot service. This process can be automated for new enterprise devices manufactured by OEMs that are Windows Autopilot partners. |
| **Add devices** | Adding a device is the process of registering a device with the Windows Autopilot service (if it isn't already registered) **and associating it to a tenant ID**. |
| **Import devices** | Importing devices is the process of uploading a comma-separated-values (CSV) file that contains device information in order to manually add devices. The device information includes information such the model and serial number. |
| **Enroll devices** | Enrolling a device is the process of adding devices to Intune. |

## Device identification

To identify a device with Windows Autopilot, the device's unique hardware hash must be captured and uploaded to the service. As previously mentioned, this step is ideally done by the hardware vendor (OEM, reseller, or distributor) automatically associating the device with an organization. It's also possible to do identify a device with a [harvesting process](add-devices.md) that collects the device's hardware hash from within a running Windows installation.

The hardware hash contains details about the device, such as:

- Manufacturer.
- Model.
- Device serial number.
- Hard drive serial number.
- Details about when the ID was generated.
- Many other attributes that can be used to uniquely identify the device.

The hardware hash changes each time it's generated because it includes details about when it was generated. When the Windows Autopilot deployment service attempts to match a device, it considers changes like that. It also considers large changes such as a new hard drive, and is still able to match successfully. But large changes to the hardware, such as a motherboard replacement, wouldn't match, so a new hash would need to be generated and uploaded.

For more information about device IDs, see the following articles:

- [Windows Autopilot device guidelines](autopilot-device-guidelines.md).
- [Add devices to a customer account](/partner-center/autopilot).

## Windows Autopilot devices

Devices that are registered with the Windows Autopilot service are displayed in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices** > **Enrollment** > **Windows** > **Windows Autopilot** > **Devices**:

> [!NOTE]
>
> Devices that are listed in Intune under **Devices** > **Windows** > **Windows devices** aren't the same as Windows Autopilot devices **Devices** > **Enrollment** > **Windows** > **Windows Autopilot** > **Devices**. Windows Autopilot devices are added to the list of **Windows devices** when both of the following are complete:
>
> - The Autopilot registration process is successful.
> - A [licensed](requirements.md?tabs=licensing) user has signed in on the device.

## Deregister a device

[!INCLUDE [Deregister an Autopilot device](includes/deregister-autopilot-device.md)]

## Related content

- [Register devices manually](add-devices.md).
