---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 2 of 10 - Install required modules to obtain Autopilot profiles from Intune
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 2 of 10 - Install required modules to obtain Autopilot profiles from Intune.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/26/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Install required modules to obtain Autopilot profiles from Intune

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)

> [!div class="checklist"]
>
> - **Step 2: Install required modules to obtain Autopilot profiles from Intune**

- Step 3: [Create JSON file for Autopilot profiles](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Install required modules to obtain Autopilot profiles from Intune

> [!NOTE]
>
> The PowerShell code snippets in this section were updated in July of 2023 to use the Microsoft Graph PowerShell modules instead of the deprecated AzureAD Graph PowerShell modules. The Microsoft Graph PowerShell modules might require approval of additional permissions in Microsoft Entra ID when they're first used. The code snippets were also updated to force using an updated version of the WindowsAutoPilot module. For more information, see [AzureAD](/powershell/module/azuread/) and [Important: Azure AD Graph Retirement and PowerShell Module Deprecation](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270).

After making sure there's a valid Autopilot profile, the next step is to download the existing Autopilot profiles from Intune as JSON files. The JSON files contain all of the information regarding the Intune tenant and the Autopilot profile. After the JSON files are downloaded from Intune, Configuration Manager packages that contain the JSON files are created. The Configuration Manager packages are then used to install the JSON file on the device during the Windows Autopilot deployment for existing devices task sequence.

The JSON file is installed on the device to the offline Windows installation during the WinPE portion of the Configuration Manager task sequence. The JSON file makes the Autopilot profile available to the Windows out-of-box experience (OOBE) so that it can run the Autopilot deployment when Windows is started for the first time. The JSON file eliminates the need for Windows OOBE to have to first download the Autopilot profile from Intune.

> [!NOTE]
>
> Windows OOBE still checks to see if there are any Autopilot profiles assigned to the device even if a JSON file is present. If the device is an Autopilot device and there's an Autopilot profile assigned to the device, the Autopilot profile is downloaded from Intune and used instead of the JSON file.

Before the Autopilot profiles are downloaded from Intune as JSON files, certain modules need to be installed on the device where the Autopilot profile will be downloaded. These modules are required to obtain the Autopilot profile from Intune. For this tutorial and to simplify the process, installation of these modules is performed on the Configuration Manager site server. However, any device with access to Intune can be used.

To install the necessary modules to download the Autopilot profiles as a JSON file, follow these steps:

1. Sign into the Configuration Manager site server or other device that can access Intune.

1. On the device, open a PowerShell window as an administrator by right-clicking on the **Start** menu and selecting **Windows PowerShell (Admin)**/**Windows Terminal (Admin)** and then selecting **Yes** at the **User Account Control** (UAC) prompt.

1. Copy the following commands by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module -Name WindowsAutopilotIntune -MinimumVersion 5.4.0 -Force
    Install-Module -Name Microsoft.Graph.Groups -Force
    Install-Module -Name Microsoft.Graph.Authentication -Force
    Install-Module Microsoft.Graph.Identity.DirectoryManagement -Force

    Import-Module -Name WindowsAutopilotIntune -MinimumVersion 5.4
    Import-Module -Name Microsoft.Graph.Groups
    Import-Module -Name Microsoft.Graph.Authentication
    Import-Module -Name Microsoft.Graph.Identity.DirectoryManagement
    ```

1. Paste the commands into the elevated PowerShell window and then select **Enter** on the keyboard to run the commands. **Enter** might need to be selected a second time to run the last command in the code block. Once all the commands run successfully, the required modules are installed.

### Verify that Autopilot profiles from Intune can be viewed

Once the required modules are installed, the following steps can be taken to verify that Autopilot profiles from Intune can be viewed:

> [!NOTE]
>
> The following steps don't export the Autopilot profiles as a JSON file. It only verifies that the Autopilot profiles can be viewed.

1. Copy the following command by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Connect-MgGraph -Scopes "Device.ReadWrite.All", "DeviceManagementManagedDevices.ReadWrite.All", "DeviceManagementServiceConfig.ReadWrite.All", "Domain.ReadWrite.All", "Group.ReadWrite.All", "GroupMember.ReadWrite.All", "User.Read"
    ```

1. Paste the command into the elevated PowerShell window and then select **Enter** on the keyboard to run the command.

1. A **Sign in to your account** window appears. Sign in with a Microsoft Entra account that has access to Intune and the Autopilot profiles.

1. Copy the following command by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    ```

1. Paste the command into the elevated PowerShell window and then select **Enter** on the keyboard to run the command.

1. All Autopilot profiles available in Intune are displayed in the PowerShell window in JSON format. Each individual Autopilot profile is encapsulated within braces (`{}`).

## Next step: Create JSON file for Autopilot profiles

> [!div class="nextstepaction"]
> [Step 3: Create JSON file for Autopilot profiles](create-json-file.md)

## Related content

For more information on installing the required modules to obtain Autopilot profiles from Intune, see the following articles:

- [Install required modules](../../existing-devices.md#install-required-modules).
