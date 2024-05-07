---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 2 of 8 - Allow users to join devices to Microsoft Entra ID
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 2 of 8 - Allow users to join devices to Microsoft Entra ID.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/07/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# User-driven Microsoft Entra join: Allow users to join devices to Microsoft Entra ID

Autopilot device preparation user-driven Microsoft Entra join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
> [!div class="checklist"]
> - **Step 2: Allow users to join devices to Microsoft Entra ID**
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow)

> [!NOTE]
>
> If you have already allowed users to join devices to Microsoft Entra ID as part of the [Windows Autopilot for pre-provisioned deployment Microsoft Entra join](../pre-provisioning/azure-ad-join-workflow.md) scenario, you can skip this step and move on to [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md).

## Allow users to join devices to Microsoft Entra ID

In order for Windows Autopilot device preparation to work, users need to be allowed to join devices to Microsoft Entra ID. Allowing users to join devices to Microsoft Entra ID can be configured in the Azure portal:

[!INCLUDE [Allow users to join devices to Microsoft Entra ID](../../includes/automatic-intune-enrollment.md)]

## Next step: Register devices as Autopilot devices

> [!div class="nextstepaction"]
> [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md)

## More information

For more information on allowing users to join devices to Microsoft Entra ID, see the following article(s):

- [Configure device settings](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
