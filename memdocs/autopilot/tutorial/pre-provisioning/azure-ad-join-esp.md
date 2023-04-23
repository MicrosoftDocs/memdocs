---
title: Windows Autopilot for pre-provisioned deployment Azure AD join - Step 5 of 9 - Configure and assign the Enrollment Status Page (ESP)
description: How to - Windows Autopilot for pre-provisioned deployment Azure AD join - Step 5 of 9 - Configure and assign the Enrollment Status Page (ESP).
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/11/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision Azure AD join: Configure and assign the Enrollment Status Page (ESP)

Autopilot for pre-provisioned deployment Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
> [!div class="checklist"]
> - **Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)**
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Technician flow](azure-ad-join-technician-flow.md)
- Step 9: [User flow](azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment Azure AD join overview](azure-ad-join-workflow.md#workflow)

> [!NOTE]
>
> If you've already configured and assigned an ESP from another Autopilot scenario and want to keep the same settings for the ESP for the pre-provisioned Azure AD join scenario, you can skip this step and move on to [Step 6: Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md).

## The Enrollment Status Page (ESP)

[!INCLUDE [How to configure and assign an Enrollment Status Page (ESP) in Intune](../includes/configure-and-assign-esp.md)]

## Next step: Create and assign a pre-provisioned Azure AD join Autopilot profile

> [!div class="nextstepaction"]
> [Step 6: Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)

## More information

[!INCLUDE [More information ESP](../includes/more-info-esp.md)]
