---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 5 of 7 - Assign applications and scripts to device group
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 5 of 7 - Assign applications and scripts to device group.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/27/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Assign applications and scripts to device group

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create a device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)

> [!div class="checklist"]
>
> - **Step 5: Assign applications and scripts to device group**

- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device (optional)](entra-join-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

## Assign applications and scripts to device group

Windows Autopilot device preparation allows deployment of up to:

- 10 managed applications
- 10 PowerShell scripts

during the out-of-box experience (OOBE) experience before the end-user is signed in for the first time. The applications and scripts specified should be the critical applications to install and critical scripts to run before the end-user can start using the device.

Any applications installed or scripts that run during a Windows Autopilot device preparation deployment should be configured to install in the **System** context since the applications are installed and the scripts ran during OOBE when no user is signed in.

In order for applications to install and the scripts run successfully, they must be assigned to the device group created for Windows Autopilot device preparation in [Step 3: Create a device group](entra-join-device-group.md).

To assign the desired applications and scripts to the device group created for Windows Autopilot device preparation:


## Next step: Create Windows Autopilot device preparation policy

> [!div class="nextstepaction"]
> [Step 6: Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)

## More information
