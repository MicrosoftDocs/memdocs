---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 8 of 10 - Speed up the deployment process (optional)
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 8 of 10 - Speed up the deployment process (optional).
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

# Windows Autopilot deployment for existing devices: Speed up the deployment process (optional)

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
> [!div class="checklist"]
> - **Step 8: Speed up the deployment process (optional)**
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md)

## Speed up the deployment process

      > [!NOTE]
      >
      > The Configuration Manager client is installed as part of the Autopilot for existing devices task sequence to support running certain tasks such as the **Install Application** or **Install Software Updates** tasks later on in the task sequence. The Configuration Manager client though is uninstalled at the end of the task sequence. If no additional tasks are needed after the **Setup Windows and ConfigMgr** task, consider following the step [Speed up the deployment process (optional)](speed-up-deployment.md) later in the tutorial. This optional step will skip installing the Configuration Manager client which will save time and avoid potential problems with the Configuration Manager having been installed on the device (despite being uninstalled).

## Next step: Run Autopilot task sequence on device

> [!div class="nextstepaction"]
> [Step 9: Run Autopilot task sequence on device](run-autopilot-task-sequence.md)

## More information

For more information on speeding up the deployment process, see the following article(s):

- [Speeding up Windows Autopilot for existing devices](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices)