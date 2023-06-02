---
title: Windows Autopilot user-driven Azure AD join - Step 7 of 8 - Assign Autopilot device to a user
description: How to - Windows Autopilot user-driven Azure AD join - Step 7 of 8 - Assign Autopilot device to a user.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/02/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Azure AD join: Assign Autopilot device to a user (optional)

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
> [!div class="checklist"]
> - **Step 7: Assign Autopilot device to a user (optional)**
- Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Azure AD join workflow, see [Windows Autopilot user-driven Azure AD join overview](azure-ad-join-workflow.md#workflow)

## Assign Autopilot device to a user (optional)

[!INCLUDE [How to assign an Autopilot device to a user](../includes/assign-autopilot-device-to-user.md)]

## Assigning Autopilot device to a user via hardware hash CSV file

[!INCLUDE [How to assign an Autopilot device to a user via hardware hash CSV file](../includes/assign-autopilot-device-to-user-via-csv.md)]

## Next step: Deploy the device

> [!div class="nextstepaction"]
> [Step 8: Deploy the device](azure-ad-join-deploy-device.md)

## More information

For more information on assigning a user to an Autopilot device, see the following article(s):

- [Assign a user to a specific Autopilot device](/mem/autopilot/enrollment-autopilot#assign-a-user-to-a-specific-autopilot-device)
