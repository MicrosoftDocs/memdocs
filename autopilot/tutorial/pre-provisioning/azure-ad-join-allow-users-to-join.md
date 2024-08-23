---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra join - Step 2 of 9 - Allow users to join devices to Microsoft Entra ID
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra join - Step 2 of 9 - Allow users to join devices to Microsoft Entra ID.
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
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision Microsoft Entra join: Allow users to join devices to Microsoft Entra ID

Windows Autopilot for pre-provisioned deployment Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)

> [!div class="checklist"]
>
> - **Step 2: Allow users to join devices to Microsoft Entra ID**

- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Technician flow](azure-ad-join-technician-flow.md)
- Step 9: [User flow](azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If users are already allowed to join devices to Microsoft Entra ID, skip this step and move on to [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md).

## Allow users to join devices to Microsoft Entra ID

In order for Windows Autopilot to work, users need to be allowed to join devices to Microsoft Entra ID. Allowing users to join devices to Microsoft Entra ID can be configured in the [Azure portal](https://portal.azure.com):

[!INCLUDE [Allow users to join devices to Microsoft Entra ID](../../includes/allow-users-to-join.md)]

> [!NOTE]
>
> This step of allowing users to join devices to Microsoft Entra ID is only needed for the Autopilot user-driven Microsoft Entra join and Autopilot for pre-provisioned deployment Microsoft Entra join scenarios. This setting doesn't apply to Microsoft Entra hybrid joined devices and Microsoft Entra joined devices using Windows Autopilot self-deployment mode as these methods work in a userless context.

## Next step: Register devices as Autopilot devices

> [!div class="nextstepaction"]
> [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md)

## Related content

[!INCLUDE [More information automatic enrollment](../../includes/more-info-allow-users-to-join.md)]
