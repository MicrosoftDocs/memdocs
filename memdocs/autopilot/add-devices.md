---
title: Adding devices
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
ms.topic: article
ms.collection: 
- M365-modern-desktop
- M365initiative-CoreDeploy
---


# Adding devices to Windows Autopilot

**Applies to**

- Windows 10

Before deploying a device using Windows Autopilot, the device must be registered with the Windows Autopilot deployment service. Ideally, this registration is performed by the OEM, reseller, or distributor from which the devices were purchased. However, the registration can also be done within your organization by collecting the hardware identity and uploading it manually.

## OEM registration

When you purchase devices from an OEM, that OEM can automatically register the devices with the Windows Autopilot. For the list of OEMs that support registration, see the "Participant device manufacturers and resellers" section of the [Windows Autopilot page](https://aka.ms/windowsautopilot).

Before an OEM can register devices for an organization, the organization must grant the OEM permission to do so. The OEM starts this process, with approval granted by an Azure AD global administrator from the organization. See the "Customer Consent" section of the [Customer consent page](registration-auth.md#oem-authorization).

> [!Note]
> While the hardware hashes (also known as hardware IDs) are generated as part of the OEM device manufacturing process, these should not be provided directly to customers or CSP partners. Instead, the OEM should register devices on the customer's behalf. In cases where devices are being registered by CSP partners, OEMs may provide PKID information to those partners to support the device registration process.

## Reseller, distributor, or partner registration

Customers may purchase devices from resellers, distributors, or other partners. As long as these resellers, distributors, and partners are part of the [Cloud Solution Partners (CSP) program](https://partner.microsoft.com/cloud-solution-provider), they too can register devices for the customer. 

As with OEMs, CSP partners must be granted permission to register devices for an organization. You can use the process described on the [Customer consent page](registration-auth.md#csp-authorization). The CSP partner requests a relationship with the organization. That organization's global administrator approves the request. After the approval, CSP partners add devices using [Partner Center](https://partner.microsoft.com/pcv/dashboard/overview), either directly through the web site or via available APIs that can automate the same tasks.

For Surface devices, Microsoft Support can help with device registration.  For more information, see [Surface Registration Support for Windows Autopilot](https://docs.microsoft.com/surface/surface-autopilot-registration-support).

Windows Autopilot doesn't require delegated administrator permissions when establishing the relationship between the CSP partner and the organization. As part of the global administrator's approval process, they can choose to uncheck the "Include delegated administration permissions" checkbox.

> [!Note]
> While resellers, distributors, or partners could boot each new Windows device to obtain the hardware hash (for purposes of providing them to customers or direct registration by the partner), this isn't recommended. Instead, these partners should register devices using the PKID information obtained from the device packaging (barcode) or obtained electronically from the OEM or upstream partner (e.g. distributor).

## Automatic registration of existing devices

You can automatically register an existing device if it's:
- running a supported version of Windows 10 semi-annual channel.
- enrolled in an MDM service such an Intune.

For devices that meet both these requirements, the MDM service can ask the device for the hardware hash. After it has that, it can automatically register the device with Windows Autopilot.

For instructions on how to do this with Microsoft Intune, see [Create an Autopilot deployment profile](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) documentation describing the "Convert all targeted devices to Autopilot" setting. 

You can automatically convert such devices to Windows using Intune's **Convert all targeted devices to Autopilot** setting. For more information, see [Create an Autopilot deployment profile](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile). 

When using the [Windows Autopilot for existing devices](existing-devices.md) scenario, you don't need to pre-register the devices with Windows Autopilot. Instead, a configuration file (AutopilotConfigurationFile.json) containing all the Windows Autopilot profile settings is used. The device can then be registered with Windows Autopilot using the same "Convert all targeted devices to Autopilot" setting.

## Manual registration

To manually register a device, you must first capture its hardware hash. Once this process has completed, the resulting hardware hash can be uploaded to the Windows Autopilot service. Because this process requires booting the device into Windows 10 to obtain the hardware hash, manual registration is intended primarily for testing and evaluation scenarios.

> [!Note]
> Customers can only register devices with a hardware hash. Other methods (PKID, tuple) are available through OEMs or CSP partners as described in the previous sections.

## Device identification

To identify a device with Windows Autopilot, the device's unique hardware hash must be captured and uploaded to the service. This step is ideally done by the hardware vendor (OEM, reseller, or distributor) automatically associating the device with an organization. It's also possible to do identify a device with a harvesting process that collects the device from within a running Windows 10 installation.

The hardware hash contains details about the device:
- manufacturer
- model
- device serial number
- hard drive serial number
- details about when the ID was generated
- many other attributes that can be used to uniquely identify the device

The hardware hash changes each time it's generated because it includes details about when it was generated. When the Windows Autopilot deployment service attempts to match a device, it considers changes like that. It also considers large changes such as a new hard drive, and is still able to match successfully. But large changes to the hardware, such as a motherboard replacement, wouldn't match, so a new hash would need to be generated and uploaded.

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
md c:\\HWID
Set-Location c:\\HWID
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
<td><a href="https://docs.microsoft.com/partner-center/autopilot">Partner Center</a></td>
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
<td><a href="https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles">Microsoft Store for Business</a></td>
<td>YES - 1000 at a time max</td>
<td>YES<b><sup>4</sup></b></td>
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Business Premium</a></td>
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


## Summary

When deploying new devices using Windows Autopilot, the following steps are required:

1. [Register devices](#registering-devices). Ideally, this step is performed by the OEM, reseller, or distributor from which the devices were purchased. However, registration can also be done by the organization by collecting the hardware identity and uploading it manually.
2. [Configure device profiles](profiles.md). Specify how the device should be deployed and what user experience should be presented.
3. Boot the device. IF the device is connected to a network with internet access, it will contact the Windows Autopilot deployment service to see if the device is registered. If it's registered, it will download profile settings such as the [Enrollment Status page](enrollment-status.md), which are used to customize the end-user experience.

## Next steps

[BitLocker encryption settings](bitlocker.md): You can configure the BitLocker encryption settings to be applied before automatic encryption is started.
