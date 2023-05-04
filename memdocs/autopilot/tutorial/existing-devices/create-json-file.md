---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 3 of 10 - Create JSON file for Autopilot profile(s)
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 3 of 10 - Create JSON file for Autopilot profile(s).
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Create JSON file for Autopilot profile(s)

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
> [!div class="checklist"]
> - **Step 3: Create JSON file for Autopilot profile(s)**
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow)

## Create JSON file for Autopilot profile(s)

Once the proper modules have been installed to allow exporting of Autopilot profile(s) from Intune, the next step is to export the Autopilot profiles as JSON files. The JSON files are used to create a package in Configuration Manager.

To export the Autopilot profiles as JSON files, follow these steps:

1. Sign into the Configuration Manager site server or other device where the required modules were installed in the [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md) step.

1. On the device, open a PowerShell window as an administrator by right clicking on the Start menu and selecting **Windows PowerShell (Admin)**/**Windows Terminal (Admin)** and then selecting **Yes** at the **User Account Control** (UAC) prompt.

1. Copy the following commands by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Connect-MSGraph
    $AutopilotProfile = Get-AutopilotProfile
    $AutopilotProfile | ForEach-Object {
    New-Item -ItemType Directory -Path "~\Desktop\$($_.displayName)"
    $_ | ConvertTo-AutopilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName)\AutopilotConfigurationFile.json"
    }
    ```

1. Paste the commands into the elevated PowerShell window and then select **Enter** on the keyboard to run the commands. If the elevated PowerShell command window isn't already signed into Intune, a **Sign in to your account** window appears. Sign in with an Azure AD account that has access to Intune and the Autopilot profiles.

1. Once signed into Intune, you may need to select **Enter** a second time to run the last command in the code block.

1. Once all the commands have run successfully, the Autopilot profile(s) appears on the Desktop in a folder with the name of the Autopilot profile from Intune. If there are multiple Autopilot profiles, each profile has its own folder on the Desktop. In each folder, there's a JSON file named **`AutopilotConfigurationFile.json`**.

> [!NOTE]
>
> The above script exports all Autopilot profiles from Intune. In addition to supported user-driven Autopilot profiles, it will also download unsupported pre-provisioning Autopilot profiles and self-deploying Autopilot profiles if they exist in the environment.

## Next step: Create and distribute package for JSON file in Configuration Manager

> [!div class="nextstepaction"]
> [Step 4: Create and distribute package for JSON file in Configuration Manager](create-json-package.md)

## More information

For more information on creating the JSON file, see the following article(s):

- [Create the JSON file](/mem/autopilot/existing-devices#create-the-json-file)
- [Get Autopilot profiles for existing devices](/mem/autopilot/existing-devices#get-autopilot-profiles-for-existing-devices)
