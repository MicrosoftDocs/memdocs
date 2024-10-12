---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 2 of 7 - Allow users to join devices to Microsoft Entra ID
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 2 of 7 - Allow users to join devices to Microsoft Entra ID.
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
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Allow users to join devices to Microsoft Entra ID

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)

> [!div class="checklist"]
>
> - **Step 2: Allow users to join devices to Microsoft Entra ID**

- Step 3: [Create a device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device (optional)](entra-join-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

> [!NOTE]
>
> If users are already allowed to join devices to Microsoft Entra ID, skip this step and move on to [Step 3: Create a device group](entra-join-device-group.md).

## Allow users to join devices to Microsoft Entra ID

In order for Windows Autopilot device preparation to work, users need to be allowed to join devices to Microsoft Entra ID. Allowing users to join devices to Microsoft Entra ID can be configured in the [Azure portal](https://portal.azure.com):

[!INCLUDE [Allow users to join devices to Microsoft Entra ID](../../../includes/allow-users-to-join.md)]

## Next step: Create a device group

> [!div class="nextstepaction"]
> [Step 3: Create a device group](entra-join-device-group.md)

## Related content

[!INCLUDE [More information automatic enrollment](../../../includes/more-info-allow-users-to-join.md)]
