---
title: Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode - Step 3 of 7 - Create an assigned device group
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode - Step 3 of 7 - Create an assigned device group.
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

# Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode: Create an assigned device group

Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](automatic-allow-users-to-join.md)

> [!div class="checklist"]
>
> - **Step 3: Create an assigned device group**

- Step 4: [Create a user group](automatic-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device](automatic-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode overview](automatic-workflow.md#workflow).

> [!NOTE]
>
> The device group created in this step is specific to Windows Autopilot device preparation. Microsoft recommends creating a device group specifically for use with Windows Autopilot device preparation instead of reusing existing device groups used in other Windows Autopilot scenarios.

## Create an assigned device group

Device groups are a collection of devices organized into a Microsoft Entra group. Device groups can be either assigned or dynamic:

- **Assigned groups** - Devices are manually added to the group and are static. Windows Autopilot device preparation only uses assigned groups.
- **Dynamic groups** - Devices are automatically added to the group based on rules. Windows Autopilot device preparation doesn't use dynamic groups.

Windows Autopilot device preparation uses a device group as part of the Windows Autopilot device preparation policy. The device group specified in the Windows Autopilot device preparation policy is an **assigned device group** where devices are added automatically during the Windows Autopilot device preparation deployment by the the Windows Autopilot device preparation process.

> [!IMPORTANT]
>
> The device group specified in the Windows Autopilot device preparation policy needs to be an **assigned security device group**.

To create an assigned security device group for use with Windows Autopilot device preparation, follow these steps:

[!INCLUDE [How to Create an assigned device group in Intune](../../../includes/create-assigned-device-group.md)]

## Next step: Create a user group

> [!div class="nextstepaction"]
> [Step 4: Create a user group](automatic-user-group.md)

## Related content

[!INCLUDE [More information device group](../../../includes/more-info-groups.md)]
