---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 1 of 7 - Set up Windows automatic Intune enrollment
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 1 of 7 - Set up Windows automatic Intune enrollment.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/03/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Set up Windows automatic Intune enrollment

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

> [!div class="checklist"]
>
> - **Step 1: Set up Windows automatic Intune enrollment**

- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create a device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device (optional)](entra-join-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

> [!NOTE]
>
> If automatic Intune enrollment is already set up, skip this step and move on to [Step 2: Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md).

## Set up Windows automatic Intune enrollment

In order for Windows Autopilot device preparation to work, devices need to be able to enroll in Intune automatically. Enrolling devices in Intune automatically can be configured in the [Azure portal](https://portal.azure.com):

[!INCLUDE [Set up Windows automatic enrollment](../../../includes/automatic-intune-enrollment.md)]

## Next step: Allow users to join devices to Microsoft Entra ID

> [!div class="nextstepaction"]
> [Step 2: Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)

## Related content

[!INCLUDE [More information automatic enrollment](../../../includes/more-info-automatic-enrollment.md)]
