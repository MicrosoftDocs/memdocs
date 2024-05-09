---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 4 of 6 - Create a user group
description: How to - Windows Autopilot device preparation  user-driven Microsoft Entra join - Step 4 of 6 - Create a user group.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/08/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Create a user group

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create a device group](entra-join-device-group.md)

> [!div class="checklist"]
> - **Step 3: Create a user group**

- Step 5: [Assign applications and scripts to device group](entra-join-assign-apps-scripts.md)
- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If you have already created device groups from another Autopilot scenario, you can skip this step and move on to [Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md). However, if you're deploying multiple different Autopilot scenarios to different devices, separate device groups are required for each Autopilot scenario.

## Create a device group

Device groups are a collection of devices organized into a Microsoft Entra group. Device groups can be either dynamic or assigned:

- **Dynamic groups** - Devices are automatically added to the group based on rules.
- **Assigned groups** - Devices are manually added to the group and are static.

Windows Autopilot device preparation uses a device group as part of the Windows Autopilot device preparation policy. The device group specified in the Windows Autopilot device preparation policy is the device group where devices are added to automatically during the Windows Autopilot device preparation deployment. In the case of the device group specified in the Windows Autopilot device preparation policy, the device group needs to be an assigned group of type security.

To create a dynamic device group for use with Windows Autopilot device preparation, follow these steps:

[!INCLUDE [How to create a device group in Intune](../../../includes/create-assigned-device-group.md)]

## Next step: Assign applications and scripts to device group

> [!div class="nextstepaction"]
> [Step 5: Assign applications and scripts to device group](entra-join-assign-apps-scripts.md)

## More information

[!INCLUDE [More information device group](../../../includes/more-info-device-group.md)]
