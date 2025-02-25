---
title: Windows Autopilot user-driven Microsoft Entra join - Step 8 of 8 - Deploy the device
description: How to - Windows Autopilot user-driven Microsoft Entra join - Step 8 of 8 - Deploy the device.
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

# User-driven Microsoft Entra join: Deploy the device

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)

> [!div class="checklist"]
>
> - **Step 8: Deploy the device**

For an overview of the Windows Autopilot user-driven Microsoft Entra join workflow, see [Windows Autopilot user-driven Microsoft Entra join overview](azure-ad-join-workflow.md#workflow).

## Deploy the device

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=eee1be56-784d-48f2-932a-2274774d6263]

Once all of the configurations for the Windows Autopilot user-driven Microsoft Entra join deployment are completed in Intune and in Microsoft Entra ID, the next step is to start the Autopilot deployment process on the device. If desired, deploy any additional applications and policies that should run during the Autopilot deployment to a device group that the device is a member of.

To start the Windows Autopilot deployment process on the device, acquire a device that is part of the device group created in the previous [Create a device group](azure-ad-join-device-group.md) step. Once the device is acquired, follow these steps:

[!INCLUDE [Network connectivity](../includes/network-connectivity.md)]

4. Once the Windows Autopilot process begins, the Microsoft Entra sign-in page appears. At the Microsoft Entra sign-in page, if a user was assigned to the device, their username might be pre-populated in this screen. Enter the Microsoft Entra credentials for the user and then select **Next** (Windows 10) or **Sign in** (Windows 11) to sign in. If necessary, proceed through the multi-factor authentication (MFA) screens.

5. After authenticating with Microsoft Entra ID, the Enrollment Status Page (ESP) appears. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

6. Once **Account setup** and the user ESP process completes, the provisioning process completes, the ESP finishes, and the desktop appears. At this point, the end-user can start using the device.

## Deployment tips

[!INCLUDE [Tips assignments](../includes/tips-assignments.md)]

[!INCLUDE [Tips Microsoft Entra join screens](../includes/tips-aadj-screens.md)]

[!INCLUDE [Tips ESP progress](../includes/tips-esp-progress.md)]
