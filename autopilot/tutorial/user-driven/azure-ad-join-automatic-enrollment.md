---
title: Windows Autopilot user-driven Microsoft Entra join - Step 1 of 8 - Set up Windows automatic Intune enrollment
description: How to - Windows Autopilot user-driven Microsoft Entra join - Step 1 of 8 - Set up Windows automatic Intune enrollment.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/26/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Microsoft Entra join: Set up Windows automatic Intune enrollment

Autopilot user-driven Microsoft Entra join steps:
> [!div class="checklist"]
> - **Step 1: Set up Windows automatic Intune enrollment**
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow)

> [!NOTE]
>
> If you have already set up automatic Intune enrollment from another Autopilot scenario, you can skip this step and move on to [Step 2: Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md).

## Set up Windows automatic Intune enrollment

[!INCLUDE [Set up Windows automatic enrollment](../includes/automatic-intune-enrollment.md)]

<a name='next-step-allow-users-to-join-devices-to-azure-ad'></a>

## Next step: Allow users to join devices to Microsoft Entra ID

> [!div class="nextstepaction"]
> [Step 2: Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)

## More information

[!INCLUDE [More information automatic enrollment](../includes/more-info-automatic-enrollment.md)]
