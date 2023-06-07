---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 10 of 10 - Deploy the device
description: How to - Windows Autopilot user-driven hybrid Azure AD join - Step 10 of 10 - Deploy the device.
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


# User-driven hybrid Azure AD join: Deploy the device

Autopilot user-driven hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
> [!div class="checklist"]
> - **Step 10: Deploy the device**

For an overview of the Windows Autopilot user-driven hybrid Azure AD join workflow, see [Windows Autopilot user-driven hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md#workflow)

## Deploy the device

Once all of the configurations for the Windows Autopilot user-driven hybrid Azure AD join deployment have been completed on the Intune and Azure AD side, the next step is to start the Autopilot deployment process on the device. If desired, deploy any additional applications and policies that should run during the Autopilot deployment to the device group that the device is a member of.

[!INCLUDE [Assignment tip](../includes/assignment-tip.md)]

To start the Autopilot deployment process on the device, select a device that is part of the device group created in the previous [Create a device group](hybrid-azure-ad-join-device-group.md) step and then follow these steps:

[!INCLUDE [Network connectivity](../includes/network-connectivity.md)]

> [!IMPORTANT]
>
> Make sure that the connected network has connectivity to both the Internet and to a domain controller. If the connected network doesn't have connectivity to a domain controller, a solution such as VPN is required to establish connectivity to a domain controller. The VPN needs to connect to a network that has connectivity to a domain controller during the ESP.

> [!NOTE]
>
> Additional screens such as License Terms, Privacy, Language, and Keyboard may appear depending on how the Autopilot profile was configured at the [Create and assign Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md) step.

1. Once the Autopilot process begins, the Azure AD sign-in page appears. At the Azure AD sign-in page, if a user was assigned to the device, their username may be pre-populated in this screen. Enter the Azure AD credentials for the user and then select **Next** (Windows 10) or **Sign in** (Windows 11) to sign in. If necessary, proceed through the multi-factor authentication (MFA) screens.

1. After authenticating with Azure AD, the Enrollment Status Page (ESP) appears. The ESP displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

    > [!TIP]
    >
    > To view and hide detailed progress information in the ESP during the provisioning process:
    >
    > - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
    > - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

1. Once the **Device setup** phase of the Device ESP is complete, user ESP begins and the **User setup** phase starts. The ESP is temporarily dismissed and the Windows sign-on screen appears:

   1. Select <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>DEL</kbd> on the keyboard to initiate Windows sign on.
   2. Enter the on-premises domain credentials for the end-user.
   3. Select <kbd>ENTER</kbd> on the keyboard to sign the end-user into the device.

    > [!IMPORTANT]
    >
    > If on-premises domain end-user credentials are different from Azure AD end-user credentials, make sure that the **on-premises domain end-user credentials** are used to sign into the device at this step. Don't use the Azure AD end-user credentials to attempt to sign into the device at this step.

1. The Enrollment Status Page (ESP) appears again and the **Account setup** phase of the user ESP continues.

   1. After a short period of time, the Azure AD sign-in page may appear. Sign in with the end-user's Azure AD credentials and then select the **Next** button.

      > [!IMPORTANT]
      >
      > If on-premises domain end-user credentials are different from Azure AD end-user credentials, make sure that **Azure AD end-user credentials** are used to sign in at this step. Don't use on-premises credentials to sign in at this step.

   1. The **Stay signed in to all your apps** screen appears. Make sure that the option **Allow my organization to manage my device** is selected, and then select **OK**.

   1. The **You're all set!** screen appears. Select **Done**.

      > [!NOTE]
      >
      > Under certain circumstances, the Azure AD sign-in and subsequent pages may not appear and the end-user may be automatically signed into Azure AD. For example, if using [Active Directory Federation Services (ADFS)](/windows-server/identity/active-directory-federation-services) and [single sign-on (SSO)](/windows-server/identity/ad-fs/operations/ad-fs-single-sign-on-settings). If the end-user is automatically signed into Azure AD, then the Autopilot deployment will proceed on to the next step automatically.

      > [!NOTE]
      >
      > If the device is left alone with no interaction during the **Account setup** phase of the ESP, the device may enter the Windows lock screen. If the device does enter the Windows lock screen during **Account setup** of the ESP, unlock the device by selecting <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>DEL</kbd> on the keyboard, entering the on-premises domain credentials for the end-user, and then selecting <kbd>ENTER</kbd> on the keyboard. Unlocking the device should go back to the Enrollment Status Page (ESP) and display the current progress of **Account setup**.

1. Once **Account setup** and the user ESP process completes, the provisioning process completes and the ESP finishes. Select the **Sign out** button to dismiss the ESP and go to the Windows sign on screen. At this point, the end-user can sign into the device using their on-premises domain end-user credentials and start using the device.

## More information
