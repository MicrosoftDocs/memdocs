---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 3 of 6 - Create a device group
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 3 of 6 - Create a device group.
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

# Windows Autopilot device preparation user-driven Microsoft Entra join: Create a device group

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)

> [!div class="checklist"]
> - **Step 3: Create a device group**

- Step 4: [Create a user group](entra-join-device-group.md)
- Step 5: [Assign applications and scripts to device group]
- Step 6: [Create and assign Windows Autopilot device preparation profile](entra-join-autopilot-profile.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow)

> [!NOTE]
>
> The device group created in this step is specific to Windows Autopilot device preparation. Microsoft recommends creating a device group specifically for use with Windows Autopilot device preparation instead of reusing existing device groups used in other Autopilot scenarios.

## Create a device group

Device groups are a collection of devices organized into a Microsoft Entra group. Device groups can be either dynamic or assigned:

- **Dynamic groups** - Devices are automatically added to the group based on rules.
- **Assigned groups** - Devices are manually added to the group and are static.

Windows Autopilot device preparation uses a device group as part of the Windows Autopilot device preparation profile. The device group specified in the Windows Autopilot device preparation profile is the device group where devices are added to automatically during the Windows Autopilot device preparation deployment. In the case of the device group specified in the Windows Autopilot device preparation profile, the device group needs to be an assigned security group.

To create an assigned security device group for use with Windows Autopilot device preparation, follow these steps:

[!INCLUDE [How to create a device group in Intune](../../../includes/create-assigned-device-group.md)]

## Next step: Configure and assign the Enrollment Status Page (ESP)

> [!div class="nextstepaction"]
> [Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)

## More information

[!INCLUDE [More information device group](../../../includes/more-info-device-group.md)]
