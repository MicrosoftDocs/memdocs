---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 3 of 7 - Create a device group
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 3 of 7 - Create a device group.
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

# Windows Autopilot device preparation user-driven Microsoft Entra join: Create a device group

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)

> [!div class="checklist"]
>
> - **Step 3: Create a device group**

- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device (optional)](entra-join-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

> [!NOTE]
>
> The device group created in this step is specific to Windows Autopilot device preparation. Microsoft recommends creating a device group specifically for use with Windows Autopilot device preparation instead of reusing existing device groups used in other Autopilot scenarios.

## Create a device group

Device groups are a collection of devices organized into a Microsoft Entra group. Device groups can be either dynamic or assigned:

- **Dynamic groups** - Devices are automatically added to the group based on rules.
- **Assigned groups** - Devices are manually added to the group and are static.

Windows Autopilot device preparation uses a device group as part of the Windows Autopilot device preparation policy. The device group specified in the Windows Autopilot device preparation policy is the device group where devices are added automatically during the Windows Autopilot device preparation deployment. The device group specified in the Windows Autopilot device preparation policy needs to be an assigned security group.

To create an assigned security device group for use with Windows Autopilot device preparation, follow these steps:

[!INCLUDE [How to create a device group in Intune](../../../includes/create-assigned-device-group.md)]

## Next step: Create a user group

> [!div class="nextstepaction"]
> [Step 4: Create a user group](entra-join-user-group.md)

## Related content

[!INCLUDE [More information device group](../../../includes/more-info-groups.md)]
