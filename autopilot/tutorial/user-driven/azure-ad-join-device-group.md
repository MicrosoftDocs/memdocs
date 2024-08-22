---
title: Windows Autopilot user-driven Microsoft Entra join - Step 4 of 8 - Create a device group
description: How to - Windows Autopilot user-driven Microsoft Entra join - Step 4 of 8 - Create a device group.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Microsoft Entra join: Create a device group

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)

> [!div class="checklist"]
>
> - **Step 4: Create a device group**

- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If device groups are already created, skip this step and move on to [Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md). However, if deploying multiple different Autopilot scenarios to different devices, separate device groups are required for each Autopilot scenario.

## Create a device group

[!INCLUDE [Device group description](../includes/device-group-description.md)]

[!INCLUDE [How to create a device group in Intune](../../includes/create-dynamic-device-group.md)]

## Next step: Configure and assign the Enrollment Status Page (ESP)

> [!div class="nextstepaction"]
> [Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)

## Related content

[!INCLUDE [More information device group](../../includes/more-info-groups.md)]
