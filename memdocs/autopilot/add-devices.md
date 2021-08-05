---
title: Manually register devices with Windows Autopilot
ms.reviewer: 
manager: laurawi
description: How to manually add devices to Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 08/05/2021
ms.topic: how-to
ms.collection: 
- M365-modern-desktop
- m365initiative-coredeploy
---


# Manually register devices with Windows Autopilot

**Applies to**

- Windows 10
- Windows Holographic, version 2004

Windows Autopilot device registration can be done within your organization by manually collecting the hardware identity of devices (hardware hashes) and uploading this information in a comma-separated-value (CSV) file. Capturing the hardware hash for manual registration requires booting the device into Windows 10. Therefore, this process is intended primarily for testing and evaluation scenarios.

Device owners can only register their devices with a hardware hash. Other methods (PKID, tuple) are available through OEMs or CSP partners.

This article provides step by step guidance to perform manual registration. For an overview of registration and manual registration, see the following topics:
- [Registration overview](registration-overview.md)
- [Manual registration overview](manual-registration.md)

For more information about registering HoloLens 2 devices with Windows Autopilot, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot#2-register-devices-in-windows-autopilot).

> [!IMPORTANT]
> In Windows 10, version 1809 and earlier, it is important to not connect devices to the Internet prior to capturing the hardware hash and creating an Autopilot device profile. This includes collecting the hardware hash, uploading the .CSV into MSfB or Intune, assigning the profile, and confirming the profile assignment. Connecting the device to the Internet before this process is complete will result in the device downloading a blank profile that is stored on the device until it's explicity removed. In Windows 10 version 1809, you can clear the cached profile by restarting OOBE. In previous versions, the only way to clear the stored profile is to re-install the OS, reimage the PC, or run **sysprep /generalize /oobe**. <br>
> <br>After Intune reports the profile ready to go, only then should the device be connected to the Internet.

> [!NOTE]
> If OOBE is restarted too many times it can enter a recovery mode and fail to run the Autopilot configuration. You can identify this scenario if OOBE displays multiple configuration options on the same page, including language, region, and keyboard layout. The normal OOBE displays each of these on a separate page. The following value key tracks the count of OOBE retries: <br>
> <br>**HKCU\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\UserOOBE** <br>
> To ensure OOBE has not been restarted too many times, you can change this value to 1.

## Prerequisites

- [Intune subscription](../intune/fundamentals/licenses.md)
- [Windows automatic enrollment enabled](../intune/enrollment/windows-enroll.md#enable-windows-10-automatic-enrollment)
- [Azure Active Directory Premium subscription](/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->

## Required permissions

Device enrollment can be done by an **Intune Administrator** or a **Policy and Profile Manager**. You can also create a custom Autopilot device manager role by using [Role Based Access Control](../intune/fundamentals/role-based-access-control.md) and creating this role. Autopilot device management only requires that you enable all permissions under **Enrollment programs**, with the exception of the four token management options.

## Collecting the hardware hash from existing devices using Microsoft Endpoint Configuration Manager

Microsoft Endpoint Configuration Manager automatically collects the hardware hashes for existing Windows 10 devices. For more information, see [Gather information from Configuration Manager for Windows Autopilot](/configmgr/comanage/how-to-prepare-win10#windows-autopilot). You can extract the hash information from Configuration Manager into a CSV file.

> [!Note]
> Before uploading the CSV file on Intune, please make sure that the first row contains the device serial number, Windows product ID, hardware hash, group tag, and assigned user. If there is header information on the top of CSV file, please delete that header information. See details at [Enroll Windows devices in Intune](/intune/enrollment/enrollment-autopilot).

## Collecting the hardware hash from existing devices using PowerShell

The hardware hash for an existing device is available through Windows Management Instrumentation (WMI), as long as that device is running a supported version of Windows 10 semi-annual channel. You can use a PowerShell script ([Get-WindowsAutoPilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)) to get a device's hardware hash and serial number. The serial number is useful to quickly see which device the hardware hash belongs to.

To use this script, you can use either of the following methods:
- Download the script file from the PowerShell Gallery and run it on each computer.
- Install the script directly from the PowerShell Gallery.

To install it directly and capture the hardware hash from the local computer, use the following commands from an elevated Windows PowerShell prompt:

```powershell
New-Item -Type Directory -Path "C:\HWID"
Set-Location -Path "C:\HWID"
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo -OutputFile AutoPilotHWID.csv
```

You can run the commands remotely if both of the following are true:
- WMI permissions are in place
- WMI is accessible through the Windows Firewall on the remote computer.

For more information about running the script, see the [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) script’s help by using “Get-Help Get-WindowsAutoPilotInfo”.

## Add devices

Now that you have captured hardware hashes in a CSV file, you can add Windows Autopilot devices by importing the CSV file. The following are instructions to import the CSV using Intune:

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program** > **Import**.

    ![Screenshot of Windows Autopilot devices](images/autopilot-import-device.png)

2. Under **Add Windows Autopilot devices**, browse to a CSV file listing the devices that you want to add. The CSV file should list:
    - Serial numbers.
    - Windows product IDs.
    - Hardware hashes.
    - Optional group tags.
    - Optional assigned user.
  
    You can have up to 500 rows in the list. The header and line format is shown below:

   `Device Serial Number,Windows Product ID,Hardware Hash,Group Tag,Assigned User`</br>
   `<serialNumber>,<ProductID>,<hardwareHash>,<optionalGroupTag>,<optionalAssignedUser>`

   ![Screenshot of Adding Windows Autopilot devices](media/enrollment-autopilot/autopilot-import-device-2.png)

   >[!IMPORTANT]
   > When you use CSV upload to assign a user, make sure that you assign valid UPNs. If you assign an invalid UPN (incorrect username), your device may be inaccessible until you remove the invalid assignment. During CSV upload the only validation we perform on the **Assigned User** column is to check that the domain name is valid. We're unable to perform individual UPN validation to ensure that you're assigning an existing or correct user.

    > [!NOTE]
    > The CSV file being imported into the Intune portal must be formatted as described above.  Extra columns are not supported.  Quotes are not supported.  Only ANSI-format text files can be used (not Unicode).  Headers are case-sensitive.  Editing the file in Excel and saving as a CSV file will not generate a usable file due to these requirements.

3. Choose **Import** to start importing the device information. Importing can take several minutes.

4. After import is complete, choose **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program** > **Sync**. A message displays that the synchronization is in progress. The process might take a few minutes to complete, depending on how many devices are being synchronized.

5. Refresh the view to see the new devices.

## Edit Autopilot device attributes

After you've uploaded an Autopilot device, you can edit certain attributes of the device.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**).
2. Select the device you want to edit.
3. In the pane on the right of the screen, you can edit:
    - Device name.
    - Group tag.
    - User Friendly Name (if you've assigned a user).
4. Select **Save**.

> [!NOTE]
> Device names can be configured for all devices, but are ignored in Hybrid Azure AD joined deployments. Device name still comes from the domain join profile for Hybrid Azure AD devices.

## Delete Autopilot devices

You can delete Windows Autopilot devices that aren't enrolled into Intune:

- Delete the devices from Windows Autopilot at **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**). Choose the devices you want to delete, then choose **Delete**. Windows Autopilot device deletion can take a few minutes to complete.

Completely removing a device from your tenant requires you to delete the Intune device, the Azure Active Directory device, and the Windows Autopilot device records. These deletions can all be done from Intune:

1. First, delete the devices from Windows Autopilot at **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**). Choose the devices you want to delete, then choose **Delete**. Windows Autopilot device deletion can take a few minutes to complete.
2. If the devices are enrolled in Intune, you must [delete them from the Intune All devices blade](../intune/remote-actions/devices-wipe.md#delete-devices-from-the-intune-portal).
3. Delete the devices in Azure Active Directory devices at **Devices** > **Azure AD devices**.

## Next steps

[Create device groups](enrollment-autopilot.md): Device groups are used to apply Autopilot deployment profiles.