---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 10 of 10 - Deploy the device
description: How to - Windows Autopilot user-driven hybrid Azure AD join - Step 10 of 10 - Deploy the device.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/05/2023
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

Once all of the configurations for the Windows Autopilot user-driven deployment have been completed on the Intune and Azure AD side, the next step is to start the Autopilot deployment process on the device. If desired, deploy any additional applications and policies that should run during the Autopilot deployment to the device group that the device is a member of.

[!INCLUDE [Assignment tip](../includes/assignment-tip.md)]

[!INCLUDE [Assignment tip](../includes/start-autopilot-deployment.md)]

     6. At this point, the device may reboot to apply critical security updates. After it reboots, the Azure AD sign-in page should appear.

    > [!NOTE]
    >
    > Additional screens such as License Terms, Privacy, Language, and Keyboard may appear before the Azure AD sign-in page depending on how the Autopilot profile was configured at the **Create and assign Autopilot profile** step.

5. Once network connectivity has been established, the Azure AD sign-in page appears. At the Azure AD sign-in page, if a user was assigned to the device, their username may be pre-populated in this screen. Enter the Azure AD credentials for the user and then select **Next** (Windows 10) or **Sign in** (Windows 11) to sign in. If necessary, proceed through the multi-factor authentication (MFA) screens.

6. The Enrollment Status Page (ESP) should appear after signing in with the Azure AD credentials. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

   The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP.

   > [!NOTE]
   >
   > To view and hide detailed progress information in the ESP during the provisioning process:
   >
   > - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
   > - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

7. Once **Account setup** and the user ESP process completes, the provisioning process completes, the ESP finishes, and the Desktop appears. At this point, the end-user can start using the device.

## More information
