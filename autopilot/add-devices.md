---
title: Manually register devices with Windows Autopilot
description: Learn how to manually add devices to Windows Autopilot.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: madakeva
manager: aaroncz
ms.date: 02/21/2025
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

## Requirements

- [Intune subscription](/mem/intune-service/fundamentals/licenses).
- [Windows automatic enrollment enabled](/mem/intune-service/enrollment/windows-enroll#enable-windows-automatic-enrollment).
- [Microsoft Entra ID P1 or P2 subscription](/azure/active-directory/active-directory-get-started-premium).

## Required permissions

Device enrollment requires *Intune Administrator* or *Policy and Profile Manager* permissions. A custom Autopilot device manager role can also be created by using [role-based access control (RBAC)](/mem/intune-service/fundamentals/role-based-access-control). Autopilot device management requires only that all permissions under **Enrollment programs** are enabled, except for the four token management options.

> [!NOTE]
>
> In both Intune Administrator and role-based access control methods, the administrative user also requires consent to use the Microsoft Intune PowerShell and Microsoft Graph PowerShell enterprise applications.

## Collect the hardware hash

The following methods are available to harvest a hardware hash from existing devices:

- Using [Microsoft Configuration Manager](#configuration-manager).

- Using [Windows PowerShell](#powershell).

- During the out-of-box experience (OOBE) by using the [Diagnostics Page](#diagnostics-page-hash-export) (Windows 11 only).

- Directly on the device using the [Access work or school](ms-settings:workplace) pane in the [Settings app](#desktop-hash-export).

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

The hardware hash for an existing device is available through Windows Management Instrumentation (WMI). The PowerShell script [Get-WindowsAutopilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo) can be used to get a device's hardware hash and serial number. The serial number is useful for quickly seeing which device the hardware hash belongs to.

To use the `Get-WindowsAutopilotInfo.ps1` script, it needs to be downloaded and then run on a device using either of the following methods:

- [Save the hardware hash locally on a devices as a CSV file](#save-the-hardware-hash-locally-on-a-device-as-a-csv-file) - the `Get-WindowsAutopilotInfo.ps1` script saves the hardware hash locally on the device as a CSV file. This method is normally used on devices that already underwent Windows Setup and OOBE.

- [Directly upload the hardware hash to a mobile device management (MDM) service such as Intune](#directly-upload-the-hardware-hash-to-an-mdm-service) - the `Get-WindowsAutopilotInfo.ps1` script directly uploads the hardware hash to the MDM service. This method is normally used on devices that are undergoing Windows Setup and OOBE.

> [!NOTE]
>
> The `Get-WindowsAutopilotInfo` script used in this section was updated in July of 2023 to use the Microsoft Graph PowerShell modules instead of the deprecated AzureAD Graph PowerShell modules. Make sure to use the latest version of the script. The Microsoft Graph PowerShell modules might require approval of additional permissions in Microsoft Entra ID when the modules are first used. For more information, see [AzureAD](/powershell/module/azuread/) and [Important: Azure AD Graph Retirement and PowerShell Module Deprecation](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270).

#### Save the hardware hash locally on a device as a CSV file

Saving the hardware hash locally on a device as a CSV file is normally done on devices that already underwent Windows Setup and OOBE. To capture and save the hardware hash locally on a device:

1. Sign into the device.

1. On the device, open an elevated Windows PowerShell prompt.

1. Run the following commands from the elevated Windows PowerShell prompt:

   ```powershell
   [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
   New-Item -Type Directory -Path "C:\HWID"
   Set-Location -Path "C:\HWID"
   $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
   Install-Script -Name Get-WindowsAutopilotInfo
   Get-WindowsAutopilotInfo -OutputFile AutopilotHWID.csv
   ```

    > [!NOTE]
    >
    > On first run, the `Get-WindowsAutopilotInfo.ps1` script prompts to approve the required app registration permissions.

The hardware hash is saved locally on the device in the directory `C:\HWID` with the filename `AutopilotHWID.csv`. The CSV file can then be used to [import the device](#add-devices) into an MDM service such as Intune.

Instead of running the PowerShell commands directly on devices, they can instead be run remotely on devices as long as the following requirements are met on the remote device:

- WMI permissions are in place.
- WMI is accessible through Windows Firewall on the remote device.

#### Directly upload the hardware hash to an MDM service

Directly uploading the hardware hash to an MDM service such as Microsoft Intune can be done on any device, but it's especially useful for a device currently undergoing Windows Setup and OOBE. To directly upload the hardware hash for a device:

1. On a device that is:

   - Currently undergoing Windows Setup and OOBE:

     1. At the sign-in prompt after OOBE starts, open a command prompt window with the keystroke <kbd>Shift</kbd>+<kbd>F10</kbd>.

     1. In the command prompt window that opens, start PowerShell by running the following command:

        ```cmd
        powershell.exe
        ```

   - Already undergone Windows Setup and OOBE:

     1. Sign into the device.

     1. Open an elevated Windows PowerShell prompt.

1. At the `PS` PowerShell command prompt, run the following PowerShell commands:

   ```powershell
   [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    Get-WindowsAutopilotInfo -Online
   ```

      If prompted to do so, agree to install **NuGet** from the **PSGallery**.

1. When the last command of `Get-WindowsAutopilotInfo -Online` runs, a Microsoft Entra ID sign-on prompt is displayed. Sign in with an account that is at least an Intune Administrator.

   > [!NOTE]
   >
   > On first run, the `Get-WindowsAutopilotInfo.ps1` script prompts to approve the required app registration permissions.

1. After the sign-in is successful, the device hash uploads automatically.

1. Verify that the hardware hash uploaded successfully and the device is showing as a registered Windows Autopilot device using the instructions in the section [Verify the hardware hash uploaded](#verify-the-hardware-hash-uploaded).

1. For devices undergoing Windows Setup and OOBE, restart the device. The device should pick up the Windows Autopilot profile and OOBE should run through the Windows Autopilot provisioning process.

#### Verify the hardware hash uploaded

To confirm the hardware hash for the device was uploaded into Intune and that the device shows as a Windows Autopilot device:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen, select **Sync** in the toolbar.

1. Wait for the sync to finish. The sync might take several minutes.

1. After the sync completes and the device appears in the device list in the **Windows Autopilot devices** screen in Intune, the device is ready for a Windows Autopilot deployment as long as a Windows Autopilot profile is assigned to the device.

> [!NOTE]
>
> Microsoft recommends registering devices through Microsoft Intune via a 4K hardware hash only for testing or other limited scenarios for the following reasons:
>
> - Availability of free and inexpensive accounts in Intune that lack robust vetting.
> - 4K hardware hashes contain sensitive information that only device owners should maintain.
>
> In most cases, instead use the Microsoft Partner Center for Windows Autopilot device registration.

For more information about running the `Get-WindowsAutopilotInfo.ps1` script, see the script's help by running the following command at PowerShell command prompt:

```powershell
Get-Help Get-WindowsAutopilotInfo
```

### Diagnostics page hash export

To export a hardware hash using the [Windows Autopilot Diagnostics Page](whats-new.md#windows-autopilot-diagnostics-page), the device must be running Windows 11.

Windows Autopilot Diagnostics are available in OOBE.

During OOBE, enter the keystroke <kbd>CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>D</kbd> to bring up the Diagnostics Page. From this page, logs can be exported to a thumb drive. The logs include a CSV file with the hardware hash.

### Desktop hash export

Sign into the device where the hardware hash needs to be exported. Once signed into the device, open the **Accounts** > **Access work or school** pane in the **Settings** app by selecting the following link:

> [!div class="nextstepaction"]
> [Access work or school](ms-settings:workplace)

Or

1. Right-click on the **Start** menu and select **Run**.

1. In the **Run** window, next to **Open:**, enter:

   ```console
   ms-settings:workplace
   ```

   and then select **OK**.

Or

1. Right-click on the **Start** menu and select **Settings**.

1. In **Settings**, select **Accounts** in the left hand pane.

1. In the **Accounts** page, select **Access work or school**.

Once the **Access work or school** pane is open in the **Settings** app, export the log files:

- Windows 11: In the **Export your management log files** section, select the **Export** button.
- Windows 10: Select the **Export your management log files** link.

The logs include a CSV file with the hardware hash. Log files are exported to the `C:\Users\Public\Documents\MDMDiagnostics` directory.

For more information, see [Collect MDM logs](/windows/client-management/mdm-collect-logs).

## Ensure that the CSV file meets requirements

Device information in the hardware hashes CSV file should include:

| Item | Required | Optional |
| --- | --- | --- |
| **Serial number** | ✅ | ❌ |
| **Windows product ID** |Partners uploading<br>into Intune. | Admins uploading<br>directly into Intune. |
| **Hardware hash** | ✅ | ❌ |
| **Group tag** | ❌ | ✅ |
| **Assigned user** | ❌ | ✅ |

The required items of serial number and hardware can be collected into an individual device CSV file using the following methods:

- The `Get-WindowsAutopilotInfo` script documented in the [Save the hardware hash locally on a device as a CSV file](#save-the-hardware-hash-locally-on-a-device-as-a-csv-file) section.
- The Desktop hash export documented in the [Desktop hash export](#desktop-hash-export) section.

The information from the individual device CSV files can be then used to create a CSV file with multiple devices to [import](#add-devices) multiple devices at once into an MDM service such as Intune.

The multiple devices CSV file can have up to 500 rows of devices. The header and line format must have the following format:

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

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen, select **Import** in the toolbar.

1. In the **Add Autopilot devices** screen:

   1. browse to the CSV file that lists the devices that need to be added.

   1. Select **Import** to start importing the device information. Importing can take several minutes.

1. After import is complete, in the **Windows Autopilot devices** screen, select **Sync** in the toolbar.

   A message says that the synchronization is in progress. The process might take a few minutes to complete, depending on how many devices are being synchronized.

1. Select **Refresh** in the toolbar until the new devices appear.

## Edit Autopilot device attributes

After an Autopilot device is uploaded, certain attributes of the device can be edited:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen, select the device that needs to be edited.

1. In the pane on the right of the screen, the following items can be edited:

   - Device name.
   - Group tag.
   - Username (if a user is assigned).

1. Select **Save**.

> [!NOTE]
>
> Device names can be configured for all devices but are ignored in Hybrid Microsoft Entra deployments. The device name still comes from the domain join profile for Hybrid Microsoft Entra devices.

## Delete Autopilot devices

Windows Autopilot devices that aren't enrolled in Intune can be deleted:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen, select the devices that need deletion, and then select **Delete** in the toolbar. The deletion process can take a few minutes to complete.

Completely removing a device from a tenant requires the device records in Intune, Microsoft Entra ID, and Windows Autopilot to all be deleted. These deletions can all be done from Intune but need to be done in the following order. For more information, see [Deregister a device](registration-overview.md#deregister-a-device).

## Troubleshooting registration failures

1. **StorageError**: This error is a generic error that can occur for various reasons. Most of the time it's not possible to determine the exact cause of the error until further investigation is done. If this error is encountered, the best course of action is to try again later. If the issue persists, contact support.

1. **ZtdDeviceAssignedToAnotherTenant**: This error occurs when the uploaded hardware hash matches a device that is already registered to a different tenant. If this error occurs, search for the serial number corresponding to the duplicate in the CSV file. Then, search for the serial number in the **Windows Autopilot devices** pane in Intune. If the device is already registered, don't import it again.

1. **ZtdDeviceAlreadyAssigned**: This error occurs when the uploaded hardware hash matches a device that is already registered to the tenant. If this error occurs, search for the serial number corresponding to the duplicate in the CSV file. Then, search for the serial number in the **Windows Autopilot devices** pane in Intune. If the device is already registered, don't import it again. If the device isn't registered, it can be imported again.

1. **ZtdDeviceDuplicated**: This error occurs when there are duplicate hardware hashes in the CSV file. Only one of the duplicates is processed, and the others result in this error. If this error occurs, look for the other duplicates of the same device to see what the actual result was. If a duplicate that was successfully processed is found, the duplicate row from the CSV file can be removed.

1. **InvalidZtdHardwareHash**: This error occurs when one or more fields in the hardware hash are invalid or empty. Both the manufacturer and serial number information need to be included. If they're not, the device can't be registered for Windows Autopilot. To check the serial number and manufacturer information, open a command prompt and run the following command:

      ```cmd
   wmic baseboard get manufacturer, serialnumber
   ```

## Related content

- [Create device groups](enrollment-autopilot.md) to apply Autopilot deployment profiles.
