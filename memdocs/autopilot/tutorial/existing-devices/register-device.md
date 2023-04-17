---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 10 of 10 - Register device for Windows Autopilot
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 10 of 10 - Register device for Windows Autopilot.
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

# Windows Autopilot deployment for existing devices: Register device for Windows Autopilot

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
> [!div class="checklist"]
> - **Step 10: Register device for Windows Autopilot**

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md)

## Register device for Windows Autopilot

Running the Autopilot for existing devices task sequence and the Autopilot deployment on a device doesn't automatically register the device for Windows Autopilot. The Autopilot profile JSON makes the Autopilot deployment available to the device and allows the device to run that particular Autopilot deployment, but it doesn't register the device for Windows Autopilot. If the device ever undergoes a reset, when it runs OOBE for the first time after the reset, it wouldn't run the Autopilot deployment even though it has previously run an Autopilot deployment.

To ensure that the device can run an Autopilot deployment after a reset, you must register the device for Windows Autopilot. You can register a device by using the following methods:

1. [Manually register devices with Windows Autopilot](../../add-devices.md). Manually registering a device includes manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

   - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot)
   - [PowerShell script](/mem/autopilot/add-devices#powershell)
   - [Diagnostics page hash export](/mem/autopilot/add-devices#diagnostics-page-hash-export)
   - [Desktop hash export](/mem/autopilot/add-devices#desktop-hash-export)



## More information

For more information on registering the device for Windows Autopilot, see the following article(s):

- [Register the device for Windows Autopilot](/mem/autopilot/existing-devices#register-the-device-for-windows-autopilot)
- [Manually register devices with Windows Autopilot](/mem/autopilot/add-devices)
