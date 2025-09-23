---
title: Windows Autopilot self-deploying mode - Step 4 of 6 - Create a device group
description: How to - Windows Autopilot self-deploying mode - Step 4 of 6 - Create a device group.
ms.date: 06/13/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Self-deploying mode: Create a device group

Windows Autopilot self-deploying mode steps:

- Step 1: [Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)
- Step 2: [Register devices as Windows Autopilot devices](self-deploying-register-device.md)

> [!div class="checklist"]
>
> - **Step 3: Create a device group**

- Step 4: [Configure and assign Windows Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
- Step 5: [Create and assign Windows Autopilot profile](self-deploying-autopilot-profile.md)
- Step 6: [Deploy the device](self-deploying-deploy-device.md)

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md#workflow).

> [!NOTE]
>
> If device groups are already created, skip this step and move on to [Step 4: Configure and assign Windows Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md). However, if deploying multiple different Windows Autopilot scenarios to different devices, separate device groups are required for each Windows Autopilot scenario.

## Create a device group

[!INCLUDE [Device group description](../includes/device-group-description.md)]

[!INCLUDE [How to create a device group in Intune](../../includes/create-dynamic-device-group.md)]

## Next step: Configure and assign the Enrollment Status Page (ESP)

> [!div class="nextstepaction"]
> [Step 4: Configure and assign Windows Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)

## Related content

[!INCLUDE [More information device group](../../includes/more-info-groups.md)]
