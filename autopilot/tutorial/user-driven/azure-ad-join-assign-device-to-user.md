---
title: Windows Autopilot user-driven Microsoft Entra join - Step 7 of 8 - Assign Windows Autopilot device to a user
description: How to - Windows Autopilot user-driven Microsoft Entra join - Step 7 of 8 - Assign Windows Autopilot device to a user.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: madakeva
manager: bpardi
ms.date: 06/13/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Microsoft Entra join: Assign Windows Autopilot device to a user (optional)

Windows Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Windows Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Windows Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Windows Autopilot profile](azure-ad-join-autopilot-profile.md)

> [!div class="checklist"]
>
> - **Step 7: Assign Windows Autopilot device to a user (optional)**

- Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

## Assign Windows Autopilot device to a user (optional)

[!INCLUDE [How to assign a Windows Autopilot device to a user](../includes/assign-autopilot-device-to-user.md)]

## Assigning Windows Autopilot device to a user via hardware hash CSV file

[!INCLUDE [How to assign a Windows Autopilot device to a user via hardware hash CSV file](../includes/assign-autopilot-device-to-user-via-csv.md)]

## Next step: Deploy the device

> [!div class="nextstepaction"]
> [Step 8: Deploy the device](azure-ad-join-deploy-device.md)

## Related content

For more information on assigning a user to a Windows Autopilot device, see the following article:

- [Assign a user to a specific Windows Autopilot device](../../enrollment-autopilot.md#assign-a-user-to-a-specific-windows-autopilot-device).
