---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 1 of 10 - Set up a Windows Autopilot profile
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 1 of 10 - Set up a Windows Autopilot profile.
ms.date: 06/13/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Set up a Windows Autopilot profile

Windows Autopilot user-driven Microsoft Entra join steps:

> [!div class="checklist"]
>
> - **Step 1: Set up a Windows Autopilot profile**

- Step 2: [Install required modules to obtain Windows Autopilot profiles from Intune](install-modules.md)
- Step 3: [Create JSON file for Windows Autopilot profiles](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Windows Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy a Windows Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Windows Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Set up a Windows Autopilot profile

Windows Autopilot deployment for existing devices isn't a Windows Autopilot deployment where a Windows Autopilot profile is downloaded and applied to a device during the out-of-box experience (OOBE) of Windows Setup. Instead, it prepares a device to receive a Windows Autopilot profile by performing the following actions:

- Wipes the device.
- Installs a fresh copy of Windows.
- Installs a JSON file that contains the information for an existing Windows Autopilot profile.

The first step in a Windows Autopilot for existing devices deployment is to make sure there's already an existing valid Windows Autopilot profile in Intune so that the JSON file can be created. Since the JSON file only supports the user-driven Microsoft Entra join and user-driven Microsoft Entra hybrid join Windows Autopilot scenarios, one of the following steps from the respective scenario workflows can be used to create a valid Windows Autopilot profile:

- [User-driven Microsoft Entra join: Create and assign user-driven Microsoft Entra join Windows Autopilot profile](../user-driven/azure-ad-join-autopilot-profile.md)
- [User-driven Microsoft Entra hybrid join: Create and assign user-driven Microsoft Entra hybrid join Windows Autopilot profile](../user-driven/hybrid-azure-ad-join-autopilot-profile.md)

> [!NOTE]
>
> In the above steps, it's not necessary to assign the Windows Autopilot profile for Windows Autopilot deployment for existing devices scenario to work. The Windows Autopilot profile only needs to be created so that the JSON file can then be created.

Once a valid Windows Autopilot profile is created and confirmed working on an existing Windows Autopilot device, then proceed to [Step 2: Install required modules to obtain Windows Autopilot profiles from Intune](install-modules.md).

## Next step: Install required modules to obtain Windows Autopilot profiles from Intune

> [!div class="nextstepaction"]
> [Step 2: Install required modules to obtain Windows Autopilot profiles from Intune](install-modules.md)

## Related content

[!INCLUDE [More information Windows Autopilot profile](../includes/more-info-autopilot-profile.md)]
