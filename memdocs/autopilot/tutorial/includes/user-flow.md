---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/07/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

azure-ad-join-user-flow.md
hybrid-azure-ad-join-user-flow.md

Headings are driven by article context. -->

Once the technician flow step of the pre-provisioning process completes successfully and the device is resealed, the device can be delivered to the end-user. The end-user then completes the normal Windows Autopilot user-driven process. This final step is know as the user flow and involves the following steps:

1. If a wired network connection is available, connect the device to the wired network connection.

2. Power on the device.

3. Once the device boots up, one of two things occurs depending on the state of network connectivity:

   - If the device is connected to a wired network and has network connectivity, the Azure AD sign-in page appears.

   - If the device isn't connected to a wired network or if it doesn't have network connectivity:

     1. The **Let's connect you to a network** screen appears. At this screen, either plug the device into a wired network (if available), or select and connect to a wireless Wi-Fi network.

     2. Once network connectivity is established, the **Next** button should become available. Select **Next**. After a few minutes, the Azure AD sign-in page appears.

    > [!IMPORTANT]
    >
    > Internet access is always required for the user flow.

    > [!NOTE]
    >
    > Depending on which screens were selected to be shown instead of hidden when the Autopilot profile was configured at the [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md) step, additional screens such as License Terms, Privacy, Language, and Keyboard may appear before the Azure AD sign-in page.

4. At the Azure AD sign-in page, if a user was assigned to the device, their username may be pre-populated in this screen. Enter the Azure AD credentials for the user and then select **Next** (Windows 10) or **Sign in** (Windows 11) to sign in. If necessary, proceed through the multi-factor authentication (MFA) screens.

      - The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases - **Device preparation**, **Device setup**, and **Account setup**. The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

        For the user flow of Windows Autopilot for pre-provisioned deployment, the **Device setup** phase of the Device ESP and the **Account setup** phase of the User ESP runs. The **Device preparation** phase of the Device ESP doesn't run during the user flow since it already ran during the [technian flow](azure-ad-join-technician-flow.md). The **Device setup** phase of the Device ESP runs again during the user flow in case any new or additional policies or applications assigned to the device became available during the time frame that the technician flow ran and when the user flow runs after the device was delivered to the end-user.

         > [!NOTE]
         >
         > To view and hide detailed progress information in the ESP during the provisioning process:
         >
         > - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
         > - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

5. Once the provisioning process completes, the ESP finishes and Desktop appears. At this point, the end-user can start using the device.
