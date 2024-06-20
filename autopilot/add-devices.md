---
title: Manually register devices with Windows Autopilot
description: Learn how to manually add devices to Windows Autopilot.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.topic: how-to
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier2
  - essentials-manage
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Manually register devices with Windows Autopilot

Within an organization, Windows Autopilot device registration required the following actions:

1. Manually collecting the hardware identity of devices, known as hardware hashes.
1. Uploading the hardware hash information in a comma-separated-values (CSV) file.

Capturing the hardware hash for manual registration requires booting the device into Windows. For this reason, this process is primarily for testing and evaluation scenarios.

Up to 500 devices can be manually registered via a CSV file uploaded through the portal. Before proceeding with additional devices, check that the previous CSV file batch is successfully registered. If transferring devices hashes from one tenant to another tenant, see [Support tip: How to transfer Windows Autopilot devices between tenants](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-transfer-windows-autopilot-devices-between/ba-p/3920555) for additional guidance.

Device owners can only register their devices with a hardware hash. Other methods (PKID, tuple) are available through OEMs or CSP partners.

This article provides step-by-step guidance for manual registration. For more information about registration, see:

- [Windows Autopilot registration overview](registration-overview.md).
- [Manual registration overview](manual-registration.md).
- [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot#2-register-devices-in-windows-autopilot).

## Prerequisites

- [Intune subscription](/mem/intune/fundamentals/licenses).
- [Windows automatic enrollment enabled](/mem/intune/enrollment/windows-enroll#enable-windows-automatic-enrollment).
- [Microsoft Entra ID P1 or P2 subscription](/azure/active-directory/active-directory-get-started-premium).

## Required permissions

Device enrollment requires *Intune Administrator* or *Policy and Profile Manager* permissions. A custom Autopilot device manager role can also be created by using [role-based access control (RBAC)](/mem/intune/fundamentals/role-based-access-control). Autopilot device management requires only that all permissions under **Enrollment programs** are enabled, except for the four token management options.

> [!NOTE]
>
> In both Intune Administrator and role-based access control methods, the administrative user also requires consent to use the Microsoft Intune PowerShell and Microsoft Graph PowerShell enterprise applications.

## Collect the hardware hash

The following methods are available to harvest a hardware hash from existing devices:

- Using [Microsoft Configuration Manager](#configuration-manager).

- Using [Windows PowerShell](#powershell).

- During the out-of-box experience (OOBE) by using the [Diagnostics Page](#diagnostics-page-hash-export) (Windows 11 only).

- From the desktop using [Settings > Accounts](#desktop-hash-export).

For a description of each method, select the link for the method.

> [!NOTE]
>
> If OOBE is restarted too many times, it can enter a recovery mode and fail to run the Autopilot configuration. This scenario can be identified if OOBE displays multiple configuration options on the same page, including language, region, and keyboard layout. The normal OOBE process displays each of these configuration options on a separate page. The following registry key value tracks the count of OOBE retries:
>
> `HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\UserOOBE`
>
> To ensure that OOBE hasn't restarted too many times, change this registry key value to `1`.

### Configuration Manager

Microsoft Configuration Manager automatically collects the hardware hashes for existing Windows devices. For more information, see [Gather information from Configuration Manager for Windows Autopilot](/configmgr/comanage/how-to-prepare-win10#windows-autopilot). The hash information can be extracted from Configuration Manager into a CSV file.

### PowerShell

The hardware hash for an existing device is available through Windows Management Instrumentation (WMI), as long as that device is running a supported version of Windows. The PowerShell script [Get-WindowsAutopilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo) can be used to get a device's hardware hash and serial number. The serial number is useful for quickly seeing which device the hardware hash belongs to.

To use this script, use either of the following methods:

- Download the script file from the PowerShell Gallery and run it on each computer.
- Install the script directly from the PowerShell Gallery.

To install the script directly and capture the hardware hash from the local computer:

1. Use the following commands from an elevated Windows PowerShell prompt:

   ```powershell
   [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
   New-Item -Type Directory -Path "C:\HWID"
   Set-Location -Path "C:\HWID"
   $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
   Install-Script -Name Get-WindowsAutopilotInfo
   Get-WindowsAutopilotInfo -OutputFile AutopilotHWID.csv
   ```

   The commands can be run remotely if both of the following are true:

   - WMI permissions are in place.
   - WMI is accessible through Windows Firewall on the remote computer.

1. While OOBE is running, the hardware hash can be uploaded with the following steps:

   1. At the sign-in prompt, opening a command prompt with Shift+F10

   1. In the command prompt window that opens, start PowerShell by running the following command:

    ```cmd
    powershell.exe
    ```

   1. At the `PS` PowerShell prompt, run the following PowerShell commands:

    ```powershell
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
    PowerShell.exe -ExecutionPolicy Bypass
    Install-Script -name Get-WindowsAutopilotInfo -Force
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
    Get-WindowsAutopilotInfo -Online
    ```

   > [!NOTE]
   >
   > The `Get-WindowsAutopilotInfo` script was updated in July of 2023 to use the Microsoft Graph PowerShell modules instead of the deprecated AzureAD Graph PowerShell modules. Make sure to use the latest version of the script. The Microsoft Graph PowerShell modules might require approval of additional permissions in Microsoft Entra ID when they're first used. For more information, see [AzureAD](/powershell/module/azuread/) and [Important: Azure AD Graph Retirement and PowerShell Module Deprecation](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270).

1. A sign-on prompt is displayed. Sign in with an account that is at least an Intune Administrator role.

1. The device hash is uploaded automatically after signing in.

1. After confirming the details of the uploaded device hash, run a sync in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Devices** > **Windows** > **Windows enrollment** > **Devices**. Under **Windows Autopilot Deployment Program**, select **Sync**.

1. After the device appears in the device list, and an Autopilot profile is assigned, restarting the device causes OOBE to run through the Windows Autopilot provisioning process.

   On first run, it prompts to approve the required app registration permissions.

> [!NOTE]
>
> Microsoft recommends registering devices through Microsoft Intune via a 4K hardware hash only for testing or other limited scenarios for the following reasons:
>
> - Availability of free and inexpensive accounts in Intune that lack robust vetting.
> - 4K hardware hashes contain sensitive information that only device owners should maintain.
>
> In most cases, use instead the Microsoft Partner Center for Autopilot device registration.

For more information about running the `Get-WindowsAutopilotInfo.ps1` script, see the script's help by using `Get-Help Get-WindowsAutopilotInfo`.

### Diagnostics page hash export

To export a hardware hash using the [Windows Autopilot Diagnostics Page](whats-new.md#windows-autopilot-diagnostics-page), the device must be running Windows 11.

Windows Autopilot Diagnostics are available in OOBE.

During OOBE, enter the keystroke <kbd>CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>D</kbd> to bring up the Diagnostics Page. From this page, logs can be exported to a thumb drive. The logs include a CSV file with the hardware hash.

### Desktop hash export

1. Right click on the Start menu and select **Settings** > **Accounts** > **Access work or school**.

1. Export log files:

   - Windows 11: In the **Export your management log files** tile, select **Export**.
   - Windows 10: Select the **Export your management log files** link.

The logs include a CSV file with the hardware hash. Log files are exported to the `C:\Users\Public\Documents\MDMDiagnostics` directory.

For more information, see [Collect MDM logs](/windows/client-management/mdm-collect-logs).

## Ensure that the CSV file meets requirements

Device information in the hardware hashes CSV file should include:

- Serial number.
- Windows product ID.
- Hardware hash.
- Optional group tag.
- Optional assigned user.

The files can have up to 500 rows of devices. The header and line format must have the following format:

```csv
Device Serial Number,Windows Product ID,Hardware Hash,Group Tag,Assigned User
<serialNumber>,<ProductID>,<hardwareHash>,<optionalGroupTag>,<optionalAssignedUser>
```

Keep these other requirements for the CSV file in mind:

- Extra columns aren't allowed.
- Quotation marks aren't allowed.
- Only ANSI-format text files are allowed. Unicode isn't allowed.
- Headers are case-sensitive.

> [!IMPORTANT]
>
> Use a plain-text editor such as Notepad with this CSV file. Don't use Microsoft Excel. Editing and saving the CSV file with Microsoft Excel doesn't generate a usable file for importing to Intune.

When a CSV file is uploaded to assign a user, make sure to assign a valid User Principal Names (UPNs). If an invalid UPN/incorrect username is uploaded, the device might be inaccessible until the invalid assignment is removed.

During upload of a CSV file, the only validation that Microsoft performs on the `Assigned User` column is to check that the domain name is valid. Microsoft doesn't perform individual UPN validation to ensure that an existing or correct user is being assigned.

## Add devices

Once the hardware hashes are captured in a CSV file, Windows Autopilot devices can be added by importing the file. To import the file by using Intune:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**) > **Import**.

   :::image type="content" source="images/autopilot-import-device.png" alt-text="Screenshot of selections in the admin center for importing Windows Autopilot devices.":::

1. Under **Add Windows Autopilot devices**, browse to the CSV file that lists the devices that need to be added.

   :::image type="content" source="media/enrollment-autopilot/autopilot-import-device-2.png" alt-text="Screenshot of the box for specifying the path to a list of Windows Autopilot devices.":::

1. Select **Import** to start importing the device information. Importing can take several minutes.

1. After import is complete, select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**) > **Sync**.

   A message says that the synchronization is in progress. The process might take a few minutes to complete, depending on how many devices are being synchronized.

1. Refresh the view to see the new devices.

## Edit Autopilot device attributes

After an Autopilot device is uploaded, certain attributes of the device can be edited:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**).

1. Select the device that needs to be edited.

1. On the pane on the right of the screen, the following items can be edited:

   - Device name.
   - Group tag.
   - Username (if a user is assigned).

1. Select **Save**.

> [!NOTE]
>
> Device names can be configured for all devices but are ignored in Hybrid Microsoft Entra deployments. The device name still comes from the domain join profile for Hybrid Microsoft Entra devices.

## Delete Autopilot devices

Windows Autopilot devices that aren't enrolled in Intune can be deleted:

1. Select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**).

2. Choose the devices that need deletion, and then select **Delete**. The deletion process can take a few minutes to complete.

Completely removing a device from a tenant requires the device records in Intune, Microsoft Entra ID, and Windows Autopilot to all be deleted. These deletions can all be done from Intune but need to be done in the following order. For more information, see [Deregister a device](registration-overview.md#deregister-a-device).

## Troubleshooting registration failures

1. **StorageError**: This error is a generic error that can occur for various reasons. Most of the time it's not possible to determine the exact cause of the error until further investigation is done. If this error is encountered, the best course of action is to try again later. If the issue persists, contact support.

1. **ZtdDeviceAssignedToAnotherTenant**: This error occurs when the uploaded hardware hash matches a device that is already registered to a different tenant. If this error occurs, search for the serial number corresponding to the duplicate in the CSV file. Then, search for the serial number in the **Windows Autopilot devices** pane in Intune. If the device is already registered, don't import it again.

1. **ZtdDeviceAlreadyAssigned**: This error occurs when the uploaded hardware hash matches a device that is already registered to the tenant. If this error occurs, search for the serial number corresponding to the duplicate in the CSV file. Then, search for the serial number in the **Windows Autopilot devices** pane in Intune. If the device is already registered, don't import it again. If the device isn't registered, it can be imported again.

1. **ZtdDeviceDuplicated**: This error occurs when there are duplicate hardware hashes in the CSV file. Only one of the duplicates is processed, and the others result in this error. If this error occurs, look for the other duplicates of the same device to see what the actual result was. If a duplicate that was successfully processed is found, the duplicate row from the CSV file can be removed.

## Related content

- [Create device groups](enrollment-autopilot.md) to apply Autopilot deployment profiles.
