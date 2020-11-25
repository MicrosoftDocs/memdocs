---
title: Windows Autopilot registration overview
ms.reviewer: 
manager: laurawi
description: How to add devices to Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.topic: how-to
ms.collection: 
- M365-modern-desktop
- m365initiative-coredeploy
---


# Windows Autopilot registration overview

**Applies to**

- Windows 10
- Windows Holographic, version 2004

Before deploying a device using Windows Autopilot, the device must be registered with the Windows Autopilot deployment service. Successful registration requires that two processes are complete:

1. The device's unique hardware hash is captured and uploaded to the Autopilot service.
2. The device is associated to an Azure tenant ID.

Ideally, both of these processes are performed by the OEM, reseller, or distributor from which the devices were purchased providing that [registration is authorized](registration-auth.md). However, the registration can also be done within your organization by collecting the hardware identity and uploading it manually.

Devices that have been registered with the Windows Autopilot service are displayed in the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices | Windows enrollment** > **Windows Autopilot Deployment Program** > **Devices**:

![Autopilot devices](images/ap-devices.png)

> [!TIP]
> Devices that are listed in Intune under **Devices** > **Windows | Windows devices** are not the same as Windows Autopilot devices. Windows Autopilot devices are added to the list of **Windows devices** when the Autopilot registration process is successful and a [licensed](licensing-requirements.md) user has signed in on the device.

For more information about registration, see the following topics:

- [OEM registration](oem-registration.md)
- [Reseller, distributor, or partner registration](partner-registration.md)
- [Automatic registration](automatic-registration.md)
- [Manual registration](manual-registration.md)

## Related topics

[Register devices manually](add-devices.md)<br>

