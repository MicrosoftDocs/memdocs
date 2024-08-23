---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 10 of 11 - User flow
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 10 of 11 - User flow.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 07/23/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision Microsoft Entra hybrid join: User flow

Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join steps:

- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector (OU)](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign Microsoft Entra hybrid join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)

> [!div class="checklist"]
>
> - **Step 11: User flow**

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join overview](hybrid-azure-ad-join-workflow.md#workflow).

## User flow

> [!IMPORTANT]
>
> The user flow portion of the Microsoft Entra hybrid join process requires connectivity to both the Internet and a domain controller. If the connected network doesn't have connectivity to a domain controller, a solution such as a VPN that has connectivity to a domain controller is required.

Once the technician flow step of the pre-provisioning process completes successfully and the device is resealed, the device can be delivered to the end-user. The end-user then completes the normal Windows Autopilot user-driven process. This final step is know as the user flow and involves the following steps:

[!INCLUDE [Network connectivity](../includes/network-connectivity.md)]

4. Once the Autopilot process begins, the Enrollment Status Page (ESP) appears. The ESP displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

    For the user flow of Windows Autopilot for pre-provisioned deployment, the **Device setup** phase of the Device ESP and the **Account setup** phase of the User ESP runs. The **Device preparation** phase of the Device ESP doesn't run during the user flow since it already ran and completed during the [Technician flow](hybrid-azure-ad-join-technician-flow.md). The **Device setup** phase of the Device ESP runs again during the user flow in case any new or additional policies or applications assigned to the device became available during the time frame that the technician flow ran and when the user flow runs after the device was delivered to the end-user.

5. Once the **Device setup** phase of the Device ESP is complete, user ESP begins and the **User setup** phase starts. The ESP is temporarily dismissed and the Windows sign-on screen appears:

   1. Enter the keystroke <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>DEL</kbd> to initiate Windows sign-on.
   1. Enter the on-premises domain credentials for the end-user.

      If on-premises domain end-user credentials are different from Microsoft Entra end-user credentials, make sure that the **on-premises domain end-user credentials** are used to sign into the device at this step. Don't use the Microsoft Entra end-user credentials to attempt to sign into the device at this step.

   1. Select <kbd>ENTER</kbd> on the keyboard to sign the end-user into the device.

6. The Enrollment Status Page (ESP) appears again and the **Account setup** phase of the user ESP continues.

   1. After a short period of time, the Microsoft Entra sign-in page might appear. Sign in with the end-user's Microsoft Entra credentials.

      If on-premises domain end-user credentials are different from Microsoft Entra end-user credentials, make sure that **Microsoft Entra end-user credentials** are used to sign in at this step. Don't use on-premises credentials to sign in at this step.

   1. Once the credentials are entered, select **Next**.

   1. The **Stay signed in to all your apps** screen appears. Make sure that the option **Allow my organization to manage my device** is selected, and then select **OK**.

   1. The **You're all set!** screen appears. Select **Done**.

      > [!NOTE]
      >
      > Under certain circumstances, the Microsoft Entra sign-in page might not appear and the end-user might be automatically signed into Microsoft Entra ID. For example, if using [Active Directory Federation Services (ADFS)](/windows-server/identity/active-directory-federation-services) and [single sign-on (SSO)](/windows-server/identity/ad-fs/operations/ad-fs-single-sign-on-settings). If the end-user is automatically signed into Microsoft Entra ID, then the Autopilot deployment will proceed on to the next step automatically.

7. Once **Account setup** and the user ESP process completes, the provisioning process completes and the ESP finishes. Select the **Sign out** button to dismiss the ESP and go to the Windows sign-on screen. At this point, the end-user can sign into the device using their on-premises domain end-user credentials and start using the device.

## User-flow tips

[!INCLUDE [Tips HAADJ screens](../includes/tips-haadj-screens.md)]

[!INCLUDE [Tips HAADJ screen lock](../includes/tips-haadj-lock.md)]

[!INCLUDE [Tips ESP progress](../includes/tips-esp-progress.md)]

[!INCLUDE [Tips wait to run User flow](../includes/tips-pre-provision-wait-user-flow.md)]

[!INCLUDE [Tips compliance resets during User flow](../includes/tips-pre-provision-compliance-user-flow.md)]

## Related content

[!INCLUDE [More information user flow](../includes/more-info-user-flow.md)]
