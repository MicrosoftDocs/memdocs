---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra join - Step 4 of 9 - Create a device group
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra join - Step 4 of 9 - Create a device group.
ms.date: 06/13/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision Microsoft Entra join: Create a device group

Windows Autopilot for pre-provisioned deployment Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Windows Autopilot devices](azure-ad-join-register-device.md)

> [!div class="checklist"]
>
> - **Step 4: Create a device group**

- Step 5: [Configure and assign Windows Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Windows Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Windows Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Technician flow](azure-ad-join-technician-flow.md)
- Step 9: [User flow](azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If device groups are already created, skip this step and move on to [Step 5: Configure and assign Windows Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md). However, if deploying multiple different Windows Autopilot scenarios to different devices, separate device groups are required for each Windows Autopilot scenario.

## Create a device group

[!INCLUDE [Device group description](../includes/device-group-description.md)]

[!INCLUDE [How to create a device group in Intune](../../includes/create-dynamic-device-group.md)]

## Next step: Configure and assign the Enrollment Status Page (ESP)

> [!div class="nextstepaction"]
> [Step 5: Configure and assign Windows Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)

## Related content

[!INCLUDE [More information device group](../../includes/more-info-groups.md)]
