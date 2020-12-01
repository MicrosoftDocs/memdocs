---
title: Manually register devices with Windows Autopilot
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


# Manually register devices with Windows Autopilot

**Applies to**

- Windows 10
- Windows Holographic, version 2004

This article provides a short summary of the device registration process and step by step guidance to perform manual registration. For an overview of Windows Autopilot device registration, see [Registration overview](registration-overview.md). 

## Manual registration process

Before deploying a device using Windows Autopilot, the device must be registered with the Windows Autopilot deployment service. Ideally, this registration is performed by the OEM, reseller, or distributor from which the devices were purchased. However, the registration can also be done within your organization by collecting the hardware identity (the hardware hash) and uploading it manually. Capturing the hardware hash for manual registration requires booting the device into Windows 10. Therefore, this process is intended primarily for testing and evaluation scenarios.

Device owners can only register thier devices with a hardware hash. Other methods (PKID, tuple) are available through OEMs or CSP partners.

> [!NOTE]
> The process for obtaining the hardware hash from HoloLens devices is different than the process for a PC. For more information about registering HoloLens 2 devices with Windows Autopilot, see [Windows Autopilot for HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot#2-register-devices-in-windows-autopilot).

### Collecting the hardware hash from existing devices using Microsoft Endpoint Configuration Manager

Microsoft Endpoint Configuration Manager automatically collects the hardware hashes for existing Windows 10 devices. For more information, see [Gather information from Configuration Manager for Windows Autopilot](/configmgr/comanage/how-to-prepare-win10#windows-autopilot). You can extract the hash information from Configuration Manager into a CSV file.

> [!Note]
> Before uploading the CSV file on Intune, please make sure that the first row contains the device serial number, Windows product ID, hardware hash, group tag, and assigned user. If there is header information on the top of CSV file, please delete that header information. See details at [Enroll Windows devices in Intune](/intune/enrollment/enrollment-autopilot).

### Collecting the hardware hash from existing devices using PowerShell

The hardware hash for an existing device is available through Windows Management Instrumentation (WMI), as long as that device is running a supported version of Windows 10 semi-annual channel. You can use a PowerShell script ([Get-WindowsAutoPilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)) to get a device's hardware hash and serial number. The serial number is useful to quickly see which device the hardware hash belongs to.

To use this script, you can use either of the following methods:
- download it from the PowerShell Gallery and run it on each computer.
- install it directly from the PowerShell Gallery.

To install it directly and capture the hardware hash from the local computer, use the following commands from an elevated Windows PowerShell prompt:

```powershell
New-Item -Type Directory -Path "C:\HWID"
Set-Location -Path "C:\HWID"
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

You can run the commands remotely if both of the following are true:
- WMI permissions are in place
- WMI is accessible through the Windows Firewall on the remote computer.

For more information about running the script, see the [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) script’s help by using “Get-Help Get-WindowsAutoPilotInfo.ps1”.

>[!IMPORTANT]
>Do not connect devices to the Internet prior to capturing the hardware hash and creating an Autopilot device profile. This includes collecting the hardware hash, uploading the .CSV into MSfB or Intune, assigning the profile, and confirming the profile assignment. Connecting the device to the Internet before this process is complete will result in the device downloading a blank profile that is stored on the device until it's explicity removed. In Windows 10 version 1809, you can clear the cached profile by restarting OOBE. In previous versions, the only way to clear the stored profile is to re-install the OS, reimage the PC, or run **sysprep /generalize /oobe**. <br>
>After Intune reports the profile ready to go, only then should the device be connected to the Internet.

>[!NOTE]
>If OOBE is restarted too many times it can enter a recovery mode and fail to run the Autopilot configuration. You can identify this scenario if OOBE displays multiple configuration options on the same page, including language, region, and keyboard layout. The normal OOBE displays each of these on a separate page. The following value key tracks the count of OOBE retries: <br>
>**HKCU\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\UserOOBE** <br>
>To ensure OOBE has not been restarted too many times, you can change this value to 1.

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
- [Device identification](#device-identification)
- [Windows Autopilot device guidelines](autopilot-device-guidelines.md)
- [Add devices to a customer account](/partner-center/autopilot)




## Next steps

[BitLocker encryption settings](bitlocker.md): You can configure the BitLocker encryption settings to be applied before automatic encryption is started.
