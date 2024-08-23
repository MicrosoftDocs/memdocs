---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra join - Step 7 of 9 - Assign Autopilot device to a user
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra join with pre-provisioning - Step 7 of 9 - Assign Autopilot device to a user.
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

# Pre-provision Microsoft Entra join: Assign Autopilot device to a user (optional)

Windows Autopilot for pre-provisioned deployment Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)

> [!div class="checklist"]
>
> - **Step 7: Assign Autopilot device to a user (optional)**

- Step 8: [Technician flow](azure-ad-join-technician-flow.md)
- Step 9: [User flow](azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

## Assign Autopilot device to a user (optional)

[!INCLUDE [How to assign an Autopilot device to a user](../includes/assign-autopilot-device-to-user.md)]

## Assigning Autopilot device to a user via hardware hash CSV file

[!INCLUDE [How to assign an Autopilot device to a user via hardware hash CSV file](../includes/assign-autopilot-device-to-user-via-csv.md)]

## Next step: Technician flow

> [!div class="nextstepaction"]
> [Step 8: Technician flow](azure-ad-join-technician-flow.md)

## Related content

For more information on assigning a user to an Autopilot device, see the following articles:

- [Assign a user to a specific Autopilot device](../../enrollment-autopilot.md#assign-a-user-to-a-specific-autopilot-device).
