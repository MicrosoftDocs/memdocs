---
title: Windows Autopilot for pre-provisioned deployment Azure AD join - Step 3 of 9 - Register devices as Autopilot devices
description: How to - Windows Autopilot for pre-provisioned deployment Azure AD join - Step 3 of 9 - Register devices as Autopilot devices.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/29/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Pre-provisioning Azure AD join: Register devices as Autopilot devices

Windows Autopilot for pre-provisioned deployment Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
> [!div class="checklist"]
> - **Step 3: Register devices as Autopilot devices**
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Technician flow](azure-ad-join-technician-flow.md)
- Step 9: [User flow](azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment Azure AD join overview](azure-ad-join-workflow.md)

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
