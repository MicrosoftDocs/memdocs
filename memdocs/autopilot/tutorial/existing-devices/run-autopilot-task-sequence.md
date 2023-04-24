---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 9 of 10 - Run Autopilot task sequence on device
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 9 of 10 - Run Autopilot task sequence on device.
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

# Windows Autopilot deployment for existing devices: Run Autopilot task sequence on device

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
> [!div class="checklist"]
> - **Step 9: Run Autopilot task sequence on device**
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow)

## Run Autopilot task sequence on device

Once the Autopilot for existing devices has been created, modified as needed, and deployed, the task sequence can be run on a device by following these steps:

1. Start the task sequence using the desired method based on how the task sequence deployment was configured:

   - Configuration Manager Software Center
   - PXE enabled distribution point
   - Task sequence bootable media

1. Allow the task sequence to complete.

1. Once the task sequence completes, the device either restarts or shuts down depending on the shutdown or restart behavior selected in one of the following two steps:

   - [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md#modify-the-task-sequence-to-account-for-sysprep-command-line-configuration).
   - [Speed up the deployment process](run-autopilot-task-sequence.md).

    The behavior of the device after the task sequence completes depends on whether the device restarted or shut down:

   - **Restart**: the device restarts as soon as the task sequence completes and then immediately boot into Windows for the first time and run OOBE. When OOBE runs, the Autopilot JSON file is processed and the Autopilot deployment starts.

   - **Shutdown**: the device shuts down and power off  as soon as the task sequence completes. Shutting down the device gives the option to further prepare the device and then deliver it to an end-user. OOBE and the Autopilot deployment start when the end-user turns on the device for the first time.

    > [!IMPORTANT]
    >
    > If the following conditions are met when the device starts back up after the task sequence completes:
    >
    > - Device is registered as an Autopilot device in Intune.
    > - Device has an Autopilot profile assigned to it in Intune.
    >
     then the Autopilot profile from Intune is downloaded to the device and is used instead of the Autopilot profile from the JSON file staged by the task sequence. The downloaded Autopilot profile from Intune has priority over the local Autopilot profile from the JSON file.

## Next step: Register device for Windows Autopilot

> [!div class="nextstepaction"]
> [Step 10: Register device for Windows Autopilot](register-device.md)

## More information

For more information on running the Autopilot task sequence on the device, see the following article(s):

- [Complete the deployment process](/mem/autopilot/existing-devices#complete-the-deployment-process)
