---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 1 of 10 - Set up a Windows Autopilot profile
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 1 of 10 - Set up a Windows Autopilot profile.
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
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Set up a Windows Autopilot profile

Autopilot user-driven Microsoft Entra join steps:

> [!div class="checklist"]
>
> - **Step 1: Set up a Windows Autopilot profile**

- Step 2: [Install required modules to obtain Autopilot profiles from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profiles](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Set up a Windows Autopilot profile

Windows Autopilot deployment for existing devices isn't an Autopilot deployment where an Autopilot profile is downloaded and applied to a device during the out-of-box experience (OOBE) of Windows Setup. Instead, it prepares a device to receive an Autopilot profile by performing the following actions:

- Wipes the device.
- Installs a fresh copy of Windows.
- Installs a JSON file that contains the information for an existing Autopilot profile.

The first step in a Windows Autopilot for existing devices deployment is to make sure there's already an existing valid Autopilot profile in Intune so that the JSON file can be created. Since the JSON file only supports the user-driven Microsoft Entra join and user-driven Microsoft Entra hybrid join Autopilot scenarios, one of the following steps from the respective scenario workflows can be used to create a valid Autopilot profile:

- [User-driven Microsoft Entra join: Create and assign user-driven Microsoft Entra join Autopilot profile](../user-driven/azure-ad-join-autopilot-profile.md)
- [User-driven Microsoft Entra hybrid join: Create and assign user-driven Microsoft Entra hybrid join Autopilot profile](../user-driven/hybrid-azure-ad-join-autopilot-profile.md)

> [!NOTE]
>
> In the above steps, it's not necessary to assign the Autopilot profile for Windows Autopilot deployment for existing devices scenario to work. The Autopilot profile only needs to be created so that the JSON file can then be created.

Once a valid Windows Autopilot profile is created and confirmed working on an existing Autopilot device, then proceed to [Step 2: Install required modules to obtain Autopilot profiles from Intune](install-modules.md).

## Next step: Install required modules to obtain Autopilot profiles from Intune

> [!div class="nextstepaction"]
> [Step 2: Install required modules to obtain Autopilot profiles from Intune](install-modules.md)

## Related content

[!INCLUDE [More information Autopilot profile](../includes/more-info-autopilot-profile.md)]
