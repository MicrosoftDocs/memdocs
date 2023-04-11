---
title: Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - User flow
description: How to - Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - User flow.
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

# Pre-provisioning Azure AD join: User flow

Windows Autopilot for pre-provisioned deployment Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Technician flow](azure-ad-join-technician-flow.md)
> [!div class="checklist"]
> - **Step 9: User flow**

For an overview of the Windows Autopilot for pre-provisioned deployment Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment Azure AD join overview](azure-ad-join-workflow.md)

## User flow

> [!IMPORTANT]
>
> The user flow Azure AD join process requires connectivity to the Internet.

Once the technician flow step of the pre-provisioning process completes successfully and the device is resealed, the device can be delivered to the end-user. The end-user then completes the normal Windows Autopilot user-driven process. This final step is know as the user flow and involves the following steps:

1. If a wired network connection is available, connect the device to the wired network connection.

1. Power on the device.

1. Once the device boots up, one of two things occurs depending on the state of network connectivity:

   - If the device is connected to a wired network and has network connectivity, the Azure AD sign-in page appears.

   - If the device isn't connected to a wired network or if it doesn't have network connectivity, it prompts to connect to a network since connectivity to the Internet is required during the user flow phase of an Azure AD join:

     1. The **Let's connect you to a network** screen appears. At this screen, either plug the device into a wired network (if available), or select and connect to a wireless Wi-Fi network.

     1. Once network connectivity is established, the **Next** button should become available. Select **Next**. After some time, the Azure AD sign-in page appears.

    > [!NOTE]
    >
    > Depending on which screens were selected to be shown instead of hidden when the Autopilot profile was configured at the [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md) step, additional screens such as License Terms, Privacy, Language, and Keyboard may appear before the Azure AD sign-in page.

1. At the Azure AD sign-in page, if a user was assigned to the device, their username may be pre-populated in this screen. Enter the Azure AD credentials for the user and then select **Next** (Windows 10) or **Sign in** (Windows 11) to sign in. If necessary, proceed through the multi-factor authentication (MFA) screens.

1. The Enrollment Status Page (ESP) appears. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

    For the user flow of Windows Autopilot for pre-provisioned deployment, the **Device setup** phase of the Device ESP and the **Account setup** phase of the User ESP runs. The **Device preparation** phase of the Device ESP doesn't run during the user flow since it already ran during the [Technian flow](azure-ad-join-technician-flow.md).

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

[!INCLUDE [More information user flow](../includes/more-info-user-flow.md)]
