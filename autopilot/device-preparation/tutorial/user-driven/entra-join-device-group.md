---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 3 of 7 - Create an assigned device group
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 3 of 7 - Create an assigned device group.
ms.date: 04/04/2025
ms.topic: tutorial
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Create an assigned device group

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)

> [!div class="checklist"]
>
> - **Step 3: Create an assigned device group**

- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device](entra-join-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

> [!NOTE]
>
> The device group created in this step is specific to Windows Autopilot device preparation. Microsoft recommends creating a device group specifically for use with Windows Autopilot device preparation instead of reusing existing device groups used in other Windows Autopilot scenarios.

## Create an assigned device group

Device groups are a collection of devices organized into a Microsoft Entra group. Normally device groups can be either assigned or dynamic:

- **Assigned groups** - Devices are manually added to the group and are static. Windows Autopilot device preparation only uses assigned groups.
- **Dynamic groups** - Devices are automatically added to the group based on rules. Windows Autopilot device preparation doesn't use dynamic groups.

Windows Autopilot device preparation uses an **assigned device group** as part of the Windows Autopilot device preparation policy. The device group specified in the Windows Autopilot device preparation policy needs to be an **assigned device group**. The the Windows Autopilot device preparation process then adds devices automatically to this assigned device group during the Windows Autopilot device preparation deployment.

> [!IMPORTANT]
>
> The device group specified in the Windows Autopilot device preparation policy needs to be an **assigned security device group**.

> [!TIP]
>
> Although the same assigned device group can be used for multiple Windows Autopilot device preparation policies, Microsoft recommends creating a separate assigned device group for each Windows Autopilot device preparation policy. For example, a different assigned device group for a user-driven scenario vs. an automatic scenario. This allows for easier management of the Windows Autopilot device preparation policies and the devices or Cloud PCs that are assigned to them.

To create an assigned security device group for use with Windows Autopilot device preparation, follow these steps:

[!INCLUDE [How to Create an assigned device group in Intune](../../../includes/create-assigned-device-group.md)]

## Next step: Create a user group

> [!div class="nextstepaction"]
> [Step 4: Create a user group](entra-join-user-group.md)

## Related content

[!INCLUDE [More information device group](../../../includes/more-info-groups.md)]
