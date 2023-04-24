---
title: Windows Autopilot user-driven Azure AD join - Step 3 of 7 - Register devices as Autopilot devices
description: How to - Windows Autopilot user-driven Azure AD join - Step 3 of 7 - Register devices as Autopilot devices.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Azure AD join: Register devices as Autopilot devices

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
> [!div class="checklist"]
> - **Step 3: Register devices as Autopilot devices**
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)

For an overview of the Windows Autopilot user-driven Azure AD join workflow, see [Windows Autopilot user-driven Azure AD join overview](azure-ad-join-workflow.md#workflow)

> [!NOTE]
>
> If you've already registered devices as Autopilot devices from another Autopilot scenario, you can skip this step and move on to [Step 4: Create a device group](azure-ad-join-device-group.md). However, be aware that if you're deploying multiple different Autopilot scenarios to different devices, separate device groups will be required for each Autopilot scenario.

## Register devices as Autopilot devices

[!INCLUDE [How to register a device as an Autopilot device in Intune](../includes/register-autopilot-device.md)]

## Next step: Create a device group

> [!div class="nextstepaction"]
> [Step 4: Create a device group](azure-ad-join-device-group.md)

## More information

[!INCLUDE [More information register Autopilot device](../includes/more-info-register-device.md)]
