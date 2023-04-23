---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 1 of 10 - Set up a Windows Autopilot deployment
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 1 of 10 - Set up a Windows Autopilot deployment.
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

# Windows Autopilot deployment for existing devices: Set up a Windows Autopilot deployment

Autopilot user-driven Azure AD join steps:
> [!div class="checklist"]
> - **Step 1: Set up a Windows Autopilot deployment**
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow)

## Set up a Windows Autopilot deployment

Windows Autopilot deployment for existing devices isn't an Autopilot deployment that applies an Autopilot profile to a device during the out of box experience (OOBE) of Windows Setup. Instead, it prepares a device to receive an Autopilot profile via an Autopilot deployment by first wiping the device and then installing a fresh copy of Windows. The Windows Autopilot deployment for existing devices process itself isn't an Autopilot profile that is processed during OOBE. For this reason, when Windows boots for the first time and goes into OOBE after being freshly installed, it needs an existing valid Autopilot deployment to complete the Autopilot process.

The first step in a Windows Autopilot deployment for existing devices is to make sure there's already an existing valid Autopilot deployment in place assigned to the device. One of the following five workflows can be used to create and assign a valid Autopilot deployment:

- [Windows Autopilot user-driven Azure AD join](../user-driven/azure-ad-join-workflow.md)
- [Windows Autopilot user-driven hybrid Azure AD join](../user-driven/hybrid-azure-ad-join-workflow.md)
- [Windows Autopilot for pre-provisioned deployment Azure AD join](../pre-provisioning/azure-ad-join-workflow.md)
- [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join](../pre-provisioning/hybrid-azure-ad-join-workflow.md)
- [Windows Autopilot self-deploying mode](../self-deploying/self-deploying-workflow.md)

Once a valid Windows Autopilot deployment has been created, assigned, and confirmed working, then proceed to [Step 2: Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md).

## Next step: Install required modules to obtain Autopilot profile(s) from Intune

> [!div class="nextstepaction"]
> [Step 2: Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)

## More information

For more information on setting up Windows Autopilot deployments, see the following article(s):
