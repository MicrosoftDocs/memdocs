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

Running the Autopilot for existing devices task sequence and the Autopilot deployment on a device doesn't automatically register the device for Windows Autopilot. The Autopilot profile JSON makes the Autopilot deployment available to the device and allows the device to run that particular Autopilot deployment, but it doesn't register the device for Windows Autopilot. If the device ever undergoes a reset, when it runs Windows Setup and OOBE for the first time after the reset, it won't run the Autopilot deployment again even though it has previously run an Autopilot deployment.

To ensure that the device can run an Autopilot deployment after a reset, you must register the device for Windows Autopilot. You can register a device by using one of the following methods:

1. [Manually register devices with Windows Autopilot](../../add-devices.md): Manually registering a device includes manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

   - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot)
   - [PowerShell script](/mem/autopilot/add-devices#powershell)
   - [Diagnostics page hash export](/mem/autopilot/add-devices#diagnostics-page-hash-export)
   - [Desktop hash export](/mem/autopilot/add-devices#desktop-hash-export)

2. In an Autopilot profile that is deployed to a device group that the device is a member of, make sure the option **Convert all targeted devices to Autopilot** is set to **Yes**. For more information on creating and assigning Autopilot profiles, see one of the following articles on creating and assigning an Autopilot profile for each of the different Autopilot scenarios:

   - [User-driven Azure AD join: Create and assign user-driven Azure AD join Autopilot profile](../user-driven/azure-ad-join-autopilot-profile.md)
   - [User-driven hybrid Azure AD join: Create and assign user-driven hybrid Azure AD join Autopilot profile](../user-driven/hybrid-azure-ad-join-autopilot-profile.md)
   - [Pre-provisioning Azure AD join: Create and assign a pre-provisioned Azure AD join Autopilot profile](../pre-provisioning/azure-ad-join-autopilot-profile.md)
   - [Pre-provisioning hybrid Azure AD join: Create and assign a pre-provisioned hybrid Azure AD join Autopilot profile](../pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md)
   - [Self-deploying mode: Create and assign self-deploying Autopilot profile](../self-deploying/self-deploying-autopilot-profile.md)

## More information

For more information on registering the device for Windows Autopilot, see the following article(s):

- [Register the device for Windows Autopilot](/mem/autopilot/existing-devices#register-the-device-for-windows-autopilot)
- [Manually register devices with Windows Autopilot](/mem/autopilot/add-devices)
- [Create an Autopilot deployment profile](/mem/autopilot/profiles#create-an-autopilot-deployment-profile)
