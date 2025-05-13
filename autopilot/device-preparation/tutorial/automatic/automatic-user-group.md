---
title: Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode - Step 4 of 7 - Create a user group
description: How to - Windows Autopilot device preparation  user-driven Microsoft Entra join - Step 4 of 7 - Create a user group.
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

# Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode: Create a user group

Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](automatic-allow-users-to-join.md)
- Step 3: [Create an assigned device group](automatic-device-group.md)

> [!div class="checklist"]
>
> - **Step 4: Create a user group**

- Step 5: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device](automatic-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 Frontline in shared mode overview](automatic-workflow.md#workflow).

> [!NOTE]
>
> The user group created in this step is specific to Windows Autopilot device preparation. Microsoft recommends creating a user group specifically for use with Windows Autopilot device preparation instead of reusing existing user groups used in other Windows Autopilot scenarios.

## Create a user group

User groups are a collection of users organized into a Microsoft Entra group. User groups can be either dynamic or assigned:

- **Dynamic groups** - Users are automatically added to the group based on rules.
- **Assigned groups** - Users are manually added to the group and are static.

Windows Autopilot device preparation uses a user group as part of the Windows Autopilot device preparation policy. The users that are members of the user group specified in the Windows Autopilot device preparation policy are the users that receive the Windows Autopilot device preparation deployment. The user group specified in the Windows Autopilot device preparation policy needs to be a security group but can be either an assigned or dynamic group.

To create a user security group for use with Windows Autopilot device preparation, follow these steps:

[!INCLUDE [How to create a user group in Intune](../../../includes/create-user-group.md)]

## Next step: Assign applications and PowerShell scripts to device group

> [!div class="nextstepaction"]
> [Step 5: Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)

## Related content

[!INCLUDE [More information device group](../../../includes/more-info-groups.md)]
