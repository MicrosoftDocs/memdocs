---
title: Windows Autopilot self-deploying mode - Step 6 of 6 - Deploy the device
description: How to - Windows Autopilot self-deploying mode - Step 5 of 5 - Step 6 of 6 - Deploy the device.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/07/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
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
> - **Step 6: Deploy the device**

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md#workflow)

## Deploy the device

> [!NOTE]
>
> Although a user isn't assigned to a device for Windows Autopilot self-deploying mode, for testing purposes, assigning at least one policy and at least one application to users is still recommended since User ESP still runs when a user first signs into the device.

Once all of the configurations for the Windows Autopilot user-driven Azure AD join deployment have been completed on the Intune and Azure AD side, the next step is to start the Autopilot deployment process on the device. If desired, deploy any additional applications and policies that should run during the Autopilot deployment to the device group that the device is a member of.

[!INCLUDE [Assignment tip](../includes/assignment-tip.md)]

To start the Autopilot deployment process on the device, follow these steps:

1. Select a device that is part of the device group created in the previous **Create a device group** step.

1. If a wired network connection is available, connect the device to the wired network connection.

1. Power on the device.

1. Once the device boots up, one of two things occurs depending on the state of network connectivity:

   - If the device is connected to a wired network and has network connectivity, the Azure AD sign-in page appears.

   - If the device isn't connected to a wired network or if it doesn't have network connectivity, it prompts to connect to a network. Connectivity to the Internet is required during the user flow phase of an Azure AD join:

    [!INCLUDE [Network connectivity](../includes/network-connectivity.md)]

    > [!NOTE]
    >
    > Additional screens such as License Terms, Privacy, Language, and Keyboard may appear before the Enrollment Status Page (ESP) depending on how the Autopilot profile was configured at the [Create and assign Autopilot profile](self-deploying-autopilot-profile.md) step.

1. At the Azure AD sign-in page, if a user was assigned to the device, their username may be pre-populated in this screen. Enter the Azure AD credentials for the user and then select **Next** (Windows 10) or **Sign in** (Windows 11) to sign in. If necessary, proceed through the multi-factor authentication (MFA) screens.

1. The Enrollment Status Page (ESP) appears. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

    > [!NOTE]
    >
    > The **Device setup** phase of the Device ESP runs again during the user flow in case any new or additional policies or applications assigned to the device became available between the technician flow phase and the user flow phase.

    > [!NOTE]
    >
    > To view and hide detailed progress information in the ESP during the provisioning process:
    >
    > - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
    > - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

1. Once **Account setup** and the user ESP process completes, the provisioning process completes, the ESP finishes, and the Desktop appears. At this point, the end-user can start using the device.

## More information