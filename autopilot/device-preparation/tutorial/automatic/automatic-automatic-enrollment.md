---
title: Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 1 of 6 - Set up Windows automatic Intune enrollment
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 1 of 6 - Set up Windows automatic Intune enrollment.
ms.date: 06/11/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation in automatic mode for Windows 365 (preview): Set up Windows automatic Intune enrollment

Windows Autopilot device preparation in automatic mode for Windows 365 steps:

> [!div class="checklist"]
>
> - **Step 1: Set up Windows automatic Intune enrollment**

- Step 2: [Create an assigned device group](automatic-device-group.md)
- Step 3: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 4: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)
- Step 5: [Create a Cloud PC provisioning policy](automatic-cloud-pc-provisioning-policy.md)
- Step 6: [Monitor the deployment](automatic-monitor.md)

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 overview](automatic-workflow.md#workflow).

> [!NOTE]
>
> If automatic Intune enrollment is already set up, skip this step and move on to [Step 2: Create an assigned device group](automatic-device-group.md).

## Set up Windows automatic Intune enrollment

In order for Windows Autopilot device preparation to work, devices need to be able to enroll in Intune automatically. Enrolling devices in Intune automatically can be configured in the [Azure portal](https://portal.azure.com):

[!INCLUDE [Set up Windows automatic enrollment](../../../includes/automatic-intune-enrollment.md)]

## Next step: Create an assigned device group

> [!div class="nextstepaction"]
> [Step 2: Create an assigned device group](automatic-device-group.md)

## Related content

[!INCLUDE [More information automatic enrollment](../../../includes/more-info-automatic-enrollment.md)]
