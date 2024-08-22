---
title: Windows Autopilot user-driven Microsoft Entra join - Step 5 of 8 - Configure and assign the Enrollment Status Page (ESP)
description: How to - Windows Autopilot user-driven Microsoft Entra join - Step 5 of 8 - Configure and assign the Enrollment Status Page (ESP).
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/28/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Microsoft Entra join: Configure and assign the Enrollment Status Page (ESP)

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)

> [!div class="checklist"]
>
> - **Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)**

- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

> [!NOTE]
>
> If an ESP is already configured, assigned, and uses the same settings for the user-driven Microsoft Entra join scenario, skip this step and move on to [Step 6: Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md).

## The Enrollment Status Page (ESP)

[!INCLUDE [How to configure and assign an Enrollment Status Page (ESP) in Intune](../includes/configure-and-assign-esp.md)]

## Next step: Create and assign user-driven Microsoft Entra join Autopilot profile

> [!div class="nextstepaction"]
> [Step 6: Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)

## Related content

[!INCLUDE [More information ESP](../includes/more-info-esp.md)]
