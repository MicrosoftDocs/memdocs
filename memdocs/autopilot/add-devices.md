---
title: Manually register devices with Windows Autopilot
description: Learn how to manually add devices to Windows Autopilot.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.topic: how-to
ms.collection: 
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
ms.technology: itpro-deploy
---

# Manually register devices with Windows Autopilot

*Applies to:*

- Windows 11
- Windows 10
- Windows Holographic, version 2004

You can perform Windows Autopilot device registration within your organization by manually collecting the hardware identity of devices (hardware hashes) and uploading this information in a comma-separated-values (CSV) file. Capturing the hardware hash for manual registration requires booting the device into Windows. So, this process is primarily for testing and evaluation scenarios.

Device owners can only register their devices with a hardware hash. Other methods (PKID, tuple) are available through OEMs or CSP partners.

This article provides step-by-step guidance for manual registration. For more information about registration, see:

- [Windows Autopilot registration overview](registration-overview.md)
- [Manual registration overview](manual-registration.md)
- [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot#2-register-devices-in-windows-autopilot)

## Prerequisites

- [Intune subscription](../intune/fundamentals/licenses.md)
- [Windows automatic enrollment enabled](../intune/enrollment/windows-enroll.md#enable-windows-automatic-enrollment)
- [Azure Active Directory Premium subscription](/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->

## Required permissions

Device enrollment requires *Intune Administrator* or *Policy and Profile Manager* permissions. You can also create a custom Autopilot device manager role by using [role-based access control](../intune/fundamentals/role-based-access-control.md). Autopilot device management requires only that you enable all permissions under **Enrollment programs**, except for the four token management options.

> [!NOTE]
> In both Intune Administrator and role-based access control methods, the administrative user also requires consent to use the Microsoft Intune PowerShell enterprise application. 

## Collect the hardware hash

The following methods are available to harvest a hardware hash from existing devices:

1. Using [Microsoft Configuration Manager](#configuration-manager)
2. Using [Windows PowerShell](#powershell)
3. During OOBE by using the [Diagnostics Page](#diagnostics-page-hash-export) (Windows 11 only)
4. From the Desktop using [Settings > Accounts](#desktop-hash-export)

Each of these methods is described below.

In *Windows 10 version 1809 and earlier*, it's important to capture the hardware hash and create an Autopilot device profile before you connect a device to the internet. Those steps include collecting the hardware hash, uploading the CSV file into Microsoft Store for Business (MSfB) or Intune, assigning the profile, and confirming the profile assignment. 

Connecting the device to the internet before this process is complete will cause the device to download a blank profile and store it until you explicitly remove it. In Windows 10 version 1809, you can clear the cached profile by restarting the Windows Out of Box Experience (OOBE). In previous versions, the only way to clear the stored profile is to reinstall the operating system, reimage the device, or run `sysprep /generalize /oobe`.

After Intune reports the profile as ready to go, you can connect the device to the internet.

> [!NOTE]
> If OOBE is restarted too many times, it can enter a recovery mode and fail to run the Autopilot configuration. You can identify this scenario if OOBE displays multiple configuration options on the same page, including language, region, and keyboard layout. The normal OOBE process displays each of these on a separate page. The following value key tracks the count of OOBE retries:
> 
> `HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\UserOOBE`
> 
> To ensure that OOBE has not been restarted too many times, you can change this value to `1`.

### Configuration Manager

Microsoft Configuration Manager automatically collects the hardware hashes for existing Windows devices. For more information, see [Gather information from Configuration Manager for Windows Autopilot](/configmgr/comanage/how-to-prepare-win10#windows-autopilot). You can extract the hash information from Configuration Manager into a CSV file.

### PowerShell

The hardware hash for an existing device is available through Windows Management Instrumentation (WMI), as long as that device is running a supported version of Windows. You can use a PowerShell script ([Get-WindowsAutopilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo)) to get a device's hardware hash and serial number. The serial number is useful for quickly seeing which device the hardware hash belongs to.

To use this script, you can use either of the following methods:

- Download the script file from the PowerShell Gallery and run it on each computer.
- Install the script directly from the PowerShell Gallery.

To install the script directly and capture the hardware hash from the local computer:

1. Use the following commands from an elevated Windows PowerShell prompt:

   ```powershell
   New-Item -Type Directory -Path "C:\HWID"
   Set-Location -Path "C:\HWID"
   $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
   Install-Script -Name Get-WindowsAutopilotInfo
   Get-WindowsAutopilotInfo -OutputFile AutopilotHWID.csv
   ```

   You can run the commands remotely if both of the following are true:

   - WMI permissions are in place.
   - WMI is accessible through Windows Firewall on the remote computer.

2. While OOBE is running, you can start uploading the hardware hash by opening a command prompt (Shift+F10 at the sign-in prompt) and using the following commands:

   ```powershell
   PowerShell.exe -ExecutionPolicy Bypass
   Install-Script -name Get-WindowsAutopilotInfo -Force
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
   Get-WindowsAutopilotInfo -Online
   ```

3. You're prompted to sign in. An account with the Intune Administrator role is sufficient, and the device hash will then be uploaded automatically. 

4. After you confirm the details of the uploaded device hash, run a sync in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**) > **Sync**. 

5. After the device appears in your device list, and an Autopilot profile is assigned, restarting the device causes OOBE to run through the Windows Autopilot provisioning process.

   On first run, you're prompted to approve the required app registration permissions.

> [!NOTE]
> Because Intune offers free (or inexpensive) accounts that lack robust vetting, and because 4K hardware hashes contain sensitive information that only device owners should maintain, we recommend registering devices through Microsoft Endpoint Manager via a 4K hardware hash only for testing or other limited scenarios. In most cases, you should instead use the Microsoft Partner Center for Autopilot device registration.

For more information about running the *Get-WindowsAutopilotInfo.ps1* script, see the script's help by using `Get-Help Get-WindowsAutopilotInfo`.

### Diagnostics page hash export

To export a hardware hash using the [Windows Autopilot Diagnostics Page](windows-autopilot-whats-new.md#windows-autopilot-diagnostics-page), the device must be running Windows 11.

Windows Autopilot Diagnostics are available in OOBE. 

During OOBE, press **Ctrl-Shift-D** to bring up the Diagnostics Page. From this page, you can export logs to a thumb drive. The logs will include a CSV file with the hardware hash.

### Desktop hash export

1. From the Windows 10 or Windows 11 Start menu, right click and select **Settings** > **Accounts** > **Access work or school**.
2. Export log files. The logs will include a CSV file with the hardware hash.
   - Windows 11: In the **Export your management log files** tile, click **Export**. 
   - Windows 10: Click the **Export your management log files** link.

Log files are exported to the Users\Public\Documents\MDMDiagnostics directory.

For more information, see [Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)

## Ensure that the CSV file meets requirements

Device information in the CSV file where you capture hardware hashes should include:

- Serial number
- Windows product ID
- Hardware hash
- Optional group tag
- Optional assigned user

You can have up to 500 rows in the file's list of devices. The header and line format must look like this:

`Device Serial Number,Windows Product ID,Hardware Hash,Group Tag,Assigned User`</br>
`<serialNumber>,<ProductID>,<hardwareHash>,<optionalGroupTag>,<optionalAssignedUser>`

Keep these other requirements for the CSV file in mind:

- You can't use extra columns. 
- You can't use quotation marks. 
- You can use only ANSI-format text files (not Unicode). 
- Headers are case-sensitive. 

> [!IMPORTANT]
> Use a plain-text editor with this CSV file, like Notepad. Don't use Microsoft Excel. Because of the requirements, editing an Excel file and saving it as `.csv` won't generate a usable file for importing to Intune.
   
When you upload a CSV file to assign a user, make sure that you assign valid User Principal Names (UPNs). If you assign an invalid UPN (that is, an incorrect username), your device might be inaccessible until you remove the invalid assignment. 

During upload of a CSV file, the only validation that Microsoft performs on the `Assigned User` column is to check that the domain name is valid. Microsoft doesn't perform individual UPN validation to ensure that you're assigning an existing or correct user.

## Add devices

Now that you've captured hardware hashes in a CSV file, you can add Windows Autopilot devices by importing the file. To import the file by using Intune:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**) > **Import**.

   ![Screenshot of selections in the admin center for importing Windows Autopilot devices.](images/autopilot-import-device.png)

2. Under **Add Windows Autopilot devices**, browse to the CSV file that lists the devices that you want to add. 

   ![Screenshot of the box for specifying the path to a list of Windows Autopilot devices.](media/enrollment-autopilot/autopilot-import-device-2.png)

3. Select **Import** to start importing the device information. Importing can take several minutes.

4. After import is complete, select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**) > **Sync**. 

   A message says that the synchronization is in progress. The process might take a few minutes to complete, depending on how many devices are being synchronized.

5. Refresh the view to see the new devices.

## Edit Autopilot device attributes

After you've uploaded an Autopilot device, you can edit certain attributes of the device:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**).
2. Select the device that you want to edit.
3. On the pane on the right of the screen, you can edit:
   - Device name
   - Group tag
   - Username (if you've assigned a user)
4. Select **Save**.

> [!NOTE]
> Device names can be configured for all devices but are ignored in Hybrid Azure Active Directory (Azure AD) deployments. The device name still comes from the domain join profile for Hybrid Azure AD devices.

## Delete Autopilot devices

You can delete Windows Autopilot devices that aren't enrolled in Intune:

1. Select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**). 
2. Choose the devices that you want to delete, and then select **Delete**. The deletion process can take a few minutes to complete.

Completely removing a device from your tenant requires you to delete the Intune, Azure AD, and Windows Autopilot device records. You can do all these deletions from Intune, in this order:

1. If the devices are enrolled in Intune, [delete them from the Intune All devices pane](../intune/remote-actions/devices-wipe.md#delete-devices-from-the-intune-admin-center).
2. Delete the devices from Windows Autopilot at **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**). Choose the devices that you want to delete, and then select **Delete**. The deletion process can take a few minutes to complete.
3. Delete the devices from Azure AD at **Devices** > **Azure AD devices**.

## Next steps

[Create device groups](enrollment-autopilot.md) to apply Autopilot deployment profiles.
