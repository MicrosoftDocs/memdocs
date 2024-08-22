---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 3 of 10 - Create JSON file for Autopilot profiles
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 3 of 10 - Create JSON file for Autopilot profiles.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Create JSON file for Autopilot profiles

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)
- Step 2: [Install required modules to obtain Autopilot profiles from Intune](install-modules.md)

> [!div class="checklist"]
>
> - **Step 3: Create JSON file for Autopilot profiles**

- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Create JSON file for Autopilot profiles

> [!NOTE]
>
> The PowerShell code snippets in this section were updated in July of 2023 to use the Microsoft Graph PowerShell modules instead of the deprecated AzureAD Graph PowerShell modules. The Microsoft Graph PowerShell modules might require approval of additional permissions in Microsoft Entra ID when they're first used. For more information, see [AzureAD](/powershell/module/azuread/) and [Important: Azure AD Graph Retirement and PowerShell Module Deprecation](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270).

Once the proper modules are installed to allow exporting of Autopilot profiles from Intune, the next step is to export the Autopilot profiles as JSON files. The JSON files are used to create a package in Configuration Manager.

To export the Autopilot profiles as JSON files, follow these steps:

1. Sign into the Configuration Manager site server or other device where the required modules were installed in the [Install required modules to obtain Autopilot profiles from Intune](install-modules.md) step.

1. On the device, open a PowerShell window as an administrator by right-clicking on the **Start** menu and selecting **Windows PowerShell (Admin)**/**Windows Terminal (Admin)** and then selecting **Yes** at the **User Account Control** (UAC) prompt.

1. Copy the following commands by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Connect-MgGraph -Scopes "Device.ReadWrite.All", "DeviceManagementManagedDevices.ReadWrite.All", "DeviceManagementServiceConfig.ReadWrite.All", "Domain.ReadWrite.All", "Group.ReadWrite.All", "GroupMember.ReadWrite.All", "User.Read"
    $AutopilotProfile = Get-AutopilotProfile
    $targetDirectory = "C:\Autopilot"
    $AutopilotProfile | ForEach-Object {
        New-Item -ItemType Directory -Path "$targetDirectory\$($_.displayName)"
        $_ | ConvertTo-AutopilotConfigurationJSON | Set-Content -Encoding Ascii "$targetDirectory\$($_.displayName)\AutopilotConfigurationFile.json"
    }
    ```

1. Paste the commands into the elevated PowerShell window and then select **Enter** on the keyboard to run the commands. If the elevated PowerShell command window isn't already signed into Intune, a **Sign in to your account** window appears. Sign in with a Microsoft Entra account that has access to Intune and the Autopilot profiles.

1. Once signed into Intune, **Enter** might need to be selected a second time to run the last command in the code block.

1. Once all the commands run successfully, the Autopilot profiles appears in a subfolder under the folder specified by the `$targetDirectory` variable. By default, the `$targetDirectory` variable is `C:\AutoPilot`, but it can be changed to another location if desired. The subfolder has the name of the Autopilot profile from Intune. If there are multiple Autopilot profiles, each profile has its own subfolder. In each folder, there's a JSON file named **`AutopilotConfigurationFile.json`**.

> [!NOTE]
>
> The above script exports all Autopilot profiles from Intune. In addition to supported user-driven Autopilot profiles, it also downloads unsupported pre-provisioning Autopilot profiles and self-deploying Autopilot profiles if they exist in the environment.

## Next step: Create and distribute package for JSON file in Configuration Manager

> [!div class="nextstepaction"]
> [Step 4: Create and distribute package for JSON file in Configuration Manager](create-json-package.md)

## Related content

For more information on creating the JSON file, see the following articles:

- [Create the JSON file](../../existing-devices.md#create-the-json-file).
- [Get Autopilot profiles for existing devices](../../existing-devices.md#get-autopilot-profiles-for-existing-devices).
