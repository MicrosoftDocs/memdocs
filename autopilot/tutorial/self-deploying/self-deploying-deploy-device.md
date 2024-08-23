---
title: Windows Autopilot self-deploying mode - Step 6 of 6 - Deploy the device
description: How to - Windows Autopilot self-deploying mode - Step 5 of 5 - Step 6 of 6 - Deploy the device.
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

# Self-deploying mode: Deploy the device

Autopilot self-deploying mode steps:

- Step 1: [Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)
- Step 2: [Register devices as Autopilot devices](self-deploying-register-device.md)
- Step 3: [Create a device group](self-deploying-device-group.md)
- Step 4: [Configure and assign Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
- Step 5: [Create and assign Autopilot profile](self-deploying-autopilot-profile.md)

> [!div class="checklist"]
>
> - **Step 6: Deploy the device**

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md#workflow).

## Deploy the device

Once all of the configurations for the Windows Autopilot self-deploying deployment are on the Intune and Microsoft Entra ID side, the next step is to start the Autopilot deployment process on the device. If desired, deploy any additional applications and policies that should run during the Autopilot deployment to a device group that the device is a member of.

To start the Windows Autopilot deployment process on the device, acquire a device that is part of the device group created in the previous [Create a device group](self-deploying-device-group.md) step. Once the device is acquired, follow these steps:

[!INCLUDE [Network connectivity](../includes/network-connectivity.md)]

4. The Enrollment Status Page (ESP) appears. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP. For Windows Autopilot self-deploying mode, only the Device ESP and its related two related phases (**Device preparation** and **Device setup**) run. User ESP and **Account setup** don't run until after the Windows Autopilot self-deploying deployment is complete and a user signs in.

5. Once **Device setup** and the device ESP process completes, the Windows Autopilot self-deploying deployment is complete, and the Windows sign-on screen appears.

6. At this point, the end-user can sign into the device using their Microsoft Entra credentials. When the user signs in, the user ESP and **Account setup** phase runs. Once user ESP and **Account setup** completes, the provisioning process completes, the desktop appears, and the end-user can start using the device.

## Deployment tips

- Before the Autopilot deployment is started, Microsoft recommends having:<br>
<br>
  - At least one type of policy and at least one application assigned to the devices.
  - At least one type of policy and at least one application assigned to the users.

  These assignments ensure proper testing of the Windows Autopilot deployment during the Device ESP phase. It might also prevent possible issues when there are either no policies or no applications assigned to the device.

- For Windows Autopilot self-deploying mode:<br>
<br>
  - Any user assigned to the device is ignored during the Windows Autopilot self-deploying deployment.
  - User ESP doesn't run until after the Windows Autopilot self-deploying deployment completes and a user signs in.

  However, for testing purposes, assigning at least one policy and at least one application to users is still recommended.

- Depending on how the Autopilot profile was configured at the [Create and assign Autopilot profile](self-deploying-autopilot-profile.md) step, the **Keyboard** screen might appear at the start of the deployment.

[!INCLUDE [Tips ESP progress](../includes/tips-esp-progress.md)]
