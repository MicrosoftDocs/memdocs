---
title: Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 2 of 6 - Create an assigned device group
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 2 of 6 - Create an assigned device group.
ms.date: 06/11/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation in automatic mode for Windows 365 (preview): Create an assigned device group

Windows Autopilot device preparation in automatic mode for Windows 365 steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)

> [!div class="checklist"]
>
> - **Step 2: Create an assigned device group**

- Step 3: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 4: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)
- Step 5: [Create a Cloud PC provisioning policy](automatic-cloud-pc-provisioning-policy.md)
- Step 6: [Monitor the deployment](automatic-monitor.md)

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 overview](automatic-workflow.md#workflow).

> [!NOTE]
>
> The device group created in this step is specific to Windows Autopilot device preparation. Microsoft recommends creating a device group specifically for use with Windows Autopilot device preparation instead of reusing existing device groups used in other Windows Autopilot scenarios.

## Create an assigned device group

Device groups are a collection of devices or Cloud PCs organized into a Microsoft Entra group. Normally device groups can be either assigned or dynamic:

- **Assigned groups** - Devices or Cloud PCs are manually added to the group and are static. Windows Autopilot device preparation only uses assigned groups.
- **Dynamic groups** - Devices or Cloud PCs are automatically added to the group based on rules. Windows Autopilot device preparation doesn't use dynamic groups.

Windows Autopilot device preparation uses an **assigned device group** as part of the Windows Autopilot device preparation policy. The device group specified in the Windows Autopilot device preparation policy needs to be an **assigned device group**. The Windows Autopilot device preparation process then adds devices or Cloud PCs automatically to this assigned device group during the Windows Autopilot device preparation deployment.

> [!IMPORTANT]
>
> The device group specified in the Windows Autopilot device preparation policy needs to be an **assigned security device group**.

> [!TIP]
>
> Although the same assigned device group can be used for multiple Windows Autopilot device preparation policies, Microsoft recommends creating a separate assigned device group for each Windows Autopilot device preparation policy. For example, a different assigned device group for a user-driven scenario vs. an automatic scenario. Creating a separate assigned device group allows for easier management of the Windows Autopilot device preparation policies and the devices or Cloud PCs that are assigned to them.

To create an assigned security device group for use with Windows Autopilot device preparation, follow these steps:

[!INCLUDE [How to Create an assigned device group in Intune](../../../includes/create-assigned-device-group.md)]

## Next step: Assign applications and PowerShell scripts to device group

> [!div class="nextstepaction"]
> [Step 3: Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)

## Related content

[!INCLUDE [More information device group](../../../includes/more-info-groups.md)]
