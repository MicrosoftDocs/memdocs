---
title: Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode - Step 2 of 7 - Allow users to join devices to Microsoft Entra ID
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode - Step 2 of 7 - Allow users to join devices to Microsoft Entra ID.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: madakeva
manager: aaroncz
ms.date: 05/14/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode: Allow users to join devices to Microsoft Entra ID

Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)

> [!div class="checklist"]
>
> - **Step 2: Allow users to join devices to Microsoft Entra ID**

- Step 3: [Create an assigned device group](automatic-device-group.md)
- Step 4: [Create a user group](automatic-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device](automatic-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode overview](automatic-workflow.md#workflow).

> [!NOTE]
>
> If users are already allowed to join devices to Microsoft Entra ID, skip this step and move on to [Step 3: Create an assigned device group](automatic-device-group.md).

## Allow users to join devices to Microsoft Entra ID

In order for Windows Autopilot device preparation to work, users need to be allowed to join devices to Microsoft Entra ID. Allowing users to join devices to Microsoft Entra ID can be configured in the [Azure portal](https://portal.azure.com):

[!INCLUDE [Allow users to join devices to Microsoft Entra ID](../../../includes/allow-users-to-join.md)]

## Next step: Create an assigned device group

> [!div class="nextstepaction"]
> [Step 3: Create an assigned device group](automatic-device-group.md)

## Related content

[!INCLUDE [More information automatic enrollment](../../../includes/more-info-allow-users-to-join.md)]
