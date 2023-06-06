---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 06/05/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-user-flow.md
user-driven/azure-ad-join-deploy-device.md

Headings are driven by article context. -->

1. If a wired network connection is available, connect the device to the wired network connection.

2. Power on the device.

3. Once the device boots up, one of two things occurs depending on the state of network connectivity:

   - If the device is connected to a wired network and has network connectivity, the Azure AD sign-in page appears.

   - If the device isn't connected to a wired network or if it doesn't have network connectivity, it prompts to connect to a network. Connectivity to the Internet is required during the user flow phase of an Azure AD join:

     1. The **Let's connect you to a network** screen appears. At this screen, either plug the device into a wired network (if available), or select and connect to a wireless Wi-Fi network.

     2. Once network connectivity is established, the **Next** button should become available. Select **Next**. After some time, the Azure AD sign-in page appears.

    > [!NOTE]
    >
    > Additional screens such as License Terms, Privacy, Language, and Keyboard may appear before the Enrollment Status Page (ESP) depending on how the Autopilot profile was configured at the [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md) step.

4. At the Azure AD sign-in page, if a user was assigned to the device, their username may be pre-populated in this screen. Enter the Azure AD credentials for the user and then select **Next** (Windows 10) or **Sign in** (Windows 11) to sign in. If necessary, proceed through the multi-factor authentication (MFA) screens.

5. The Enrollment Status Page (ESP) appears. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

    For the user flow of Windows Autopilot for pre-provisioned deployment, the **Device setup** phase of the Device ESP and the **Account setup** phase of the User ESP runs. The **Device preparation** phase of the Device ESP doesn't run during the user flow since it already ran during the [Technician flow](azure-ad-join-technician-flow.md).

    > [!NOTE]
    >
    > The **Device setup** phase of the Device ESP runs again during the user flow in case any new or additional policies or applications assigned to the device became available between the technician flow phase and the user flow phase.

    > [!NOTE]
    >
    > To view and hide detailed progress information in the ESP during the provisioning process:
    >
    > - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
    > - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

6. Once **Account setup** and the user ESP process completes, the provisioning process completes, the ESP finishes, and the Desktop appears. At this point, the end-user can start using the device.