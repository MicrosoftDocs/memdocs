---
title: Manual registration
ms.reviewer: 
manager: laurawi
description: Manual registration overview
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

# Manual registration overview

**Applies to**

- Windows 10
- Windows Holographic, version 2004

Ideally, registration of a device with Windows Autopilot is performed by the OEM, reseller, or distributor from which the device was purchased. However it is also possible to register devices manually. You might need to register a device manually if:
- The device was obtained from a non-participant device manufacturer or reseller.
- The device is a virtual machine (VM).
- The device does not otherwise qualify for automatic registraton, such as an existing legacy device.

For a list of participant device manufacturers and device resellers, see [Autopilot device manufacturers and resellers](https://www.microsoft.com/microsoft-365/windows/windows-autopilot#office-SecondaryMessaging-k4if896).

To [manually register a device](add-devices.md), you must first capture its hardware hash. Once this process has completed, the resulting hardware hash can be uploaded to the Windows Autopilot service. Because this process requires booting the device into Windows 10 to obtain the hardware hash, manual registration is intended primarily for testing and evaluation scenarios.

> [!Note]
> Customers can only register devices with a hardware hash. Other methods (PKID, tuple) are available through OEMs or CSP partners as described in the previous sections.

## Registering devices

<img src="./images/image2.png" width="511" height="249" alt="process" />

After the hardware hashes have been captured from existing devices, they can be uploaded in any of the following ways:

- [Microsoft Intune](enrollment-autopilot.md). This is the preferred mechanism for all customers.
  - The Microsoft Endpoint Manager admin center is used for Intune device enrollment.
- [Partner Center](https://msdn.microsoft.com/partner-center/autopilot). This is used by CSP partners to register devices on behalf of customers.
- [Microsoft 365 Business & Office 365 Admin](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa). This is typically used by small and medium businesses (SMBs) who manage their devices using Microsoft 365 Business.
- [Microsoft Store for Business](/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles). You might already be using MSfB to manage your apps and settings.

A summary of each platform's capabilities is provided below.<br>
<br>
<table>
<tr>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Platform/Portal</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Register devices?</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Create/Assign profile</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Acceptable DeviceID</font></td>
</tr>

<tr>
<td>OEM Direct API</td>
<td>YES - 1000 at a time max</td>
<td>NO</td>
<td>Tuple or PKID</td>
</tr>

<tr>
<td><a href="/partner-center/autopilot">Partner Center</a></td>
<td>YES - 1000 at a time max</td>
<td>YES<b><sup>34</sup></b></td>
<td>Tuple or PKID or 4K HH</td>
</tr>

<tr>
<td><a href="enrollment-autopilot.md">Intune</a></td>
<td>YES - 500 at a time max<b><sup>1</sup></b></td> 
<td>YES<b><sup>12</sup></b></td> 
<td>4K HH</td>
</tr>

<tr>
<td><a href="/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles">Microsoft Store for Business</a></td>
<td>YES - 1000 at a time max</td>
<td>YES<b><sup>4</sup></b></td>
<td>4K HH</td>
</tr>

<tr>
<td><a href="/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Business Premium</a></td>
<td>YES - 1000 at a time max</td>
<td>YES<b><sup>3</sup></b></td>
<td>4K HH</td>
</tr>

</table>

><b><sup>1</sup></b>Microsoft recommended platform to use<br>
><b><sup>2</sup></b>Intune license required<br>
><b><sup>3</sup></b>Feature capabilities are limited<br>
><b><sup>4</sup></b>Device profile assignment will be retired from MSfB and Partner Center in the coming months<br>

For more information about device IDs, see the following topics:
- [Device identification](registration-overview.md#device-identification)
- [Windows Autopilot device guidelines](autopilot-device-guidelines.md)
- [Add devices to a customer account](/partner-center/autopilot)

## Also see

[Registration overview](registration-overview.md)<br>
[Manually register devices with Windows Autopilot](add-devices.md)