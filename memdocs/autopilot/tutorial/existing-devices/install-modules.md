---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 2 of 10 - Install required modules to obtain Autopilot profile(s) from Intune
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 2 of 10 - Install required modules to obtain Autopilot profile(s) from Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/11/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Install required modules to obtain Autopilot profile(s) from Intune

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
> [!div class="checklist"]
> - **Step 2: Install required modules to obtain Autopilot profile(s) from Intune**
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md)

## Install required modules to obtain Autopilot profile(s) from Intune

After making sure there is a valid Autopilot deployment assigned to the device, the next step is to download existing Autopilot profiles from Intune. These Autopilot profiles are downloaded as JSON files. The JSON files contain all of the information regarding the Intune tenant and the Autopilot deployment. The JSON file is pre-installed on the device to the offline Windows installation during the WinPE portion of the Configuration Manager task sequence. The pre-installed JSON file makes the Autopilot profile available to Windows OOBE so that it can run the Autopilot deployment when Windows is started for the first time.

However, before downloading the Autopilot profile as a JSON file from Intune, certain modules need to be installed on the device where the Autopilot profile will be downloaded. These modules are required to obtain the Autopilot profile from Intune. These modules can be installed on any device that can access to Intune, but for this tutorial and to simplify the process, it will guide through installing these modules on the Configuration Manager site server.

To install the necessary modules to download the Autopilot profile(s) as a JSON file, follow these steps:

1. Sign into the Configuration Manager site server or other device that can access Intune.

2. On the device, open a PowerShell window as an administrator by right clicking on the Start menu and selecting **Windows PowerShell (Admin)**/**Windows Terminal (Admin)** and then selecting **Yes** at the **User Account Control** (UAC) prompt.

3. Copy the following commands by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module AzureAD -Force
    Install-Module Microsoft.Graph.Intune -Force
    Install-Module WindowsAutopilotIntune -Force

    Import-Module AzureAD
    Import-Module Microsoft.Graph.Intune
    Import-Module WindowsAutopilotIntune
    ```

4. Paste the commands into the elevated PowerShell window and then select **Enter** on the keyboard to run the commands. Note that you may need to select **Enter** a second time to run the last command in the code block. Once all the commands have run successfully, the required modules are installed.

### Verify that Autopilot profile(s) from Intune can be viewed

Once the required modules are installed, the following steps can be taken to verify that Autopilot profile(s) from Intune can be viewed:

> [!NOTE]
>
> The following steps doesn't export the Autopilot profile(s) as a JSON file. It only verifies that the Autopilot profile(s) can be viewed.

1. Copy the following command by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Connect-MSGraph
    ```

1. Paste the command into the elevated PowerShell window and then select **Enter** on the keyboard to run the command.

1. A **Sign in to your account** window appears. Sign in with an Azure AD account that has access to Intune and the Autopilot profiles.

1. Copy the following command by selecting **Copy** at the top right corner of the below **PowerShell** code block:

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    ```

1. Paste the command into the elevated PowerShell window and then select **Enter** on the keyboard to run the command.

1. All Autopilot profiles available in Intune are displayed in the PowerShell window in JSON format. Each individual Autopilot profile is encapsulated within braces (`{}`).

## Next step: Create JSON file for Autopilot profile(s)

> [!div class="nextstepaction"]
> [Step 3: Create JSON file for Autopilot profile(s)](create-json-file.md)

## More information

For more information on installing the required modules to obtain Autopilot profiles from Intune, see the following article(s):

- [Install required modules](/mem/autopilot/existing-devices#install-required-modules)
