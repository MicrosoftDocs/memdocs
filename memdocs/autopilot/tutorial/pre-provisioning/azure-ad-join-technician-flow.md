---
title: Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - Technician flow
description: How to - Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - Technician flow.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/29/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Pre-provisioning Azure AD join: Technician flow

Windows Autopilot for pre-provisioned deployment Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
> [!div class="checklist"]
> - **Step 8: Technician flow**
- Step 9: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment Azure AD join overview](azure-ad-join-workflow.md)

## Technician flow

Once all of the configurations for Windows Autopilot for pre-provisioned deployment have been completed on the Intune and Azure AD side, the next steps is to start the Autopilot process. This steps is known as the Technician flow. To start the Technician flow, follow the below steps:

1. Boot a device that is part of the device group created in the previous **Create a device group** step.

1. From the first OOBE screen, **DON'T** select **Next**. The first OOBE screen can be a language selection screen, a locale selection screen, or the Azure AD sign-in page. Instead of selecting **Next**, press the <kbd>WIN</kbd> key five times. Pressing the <kbd>WIN</kbd> key five times should display an alternative options screen.

1. From the alternative options screen, select the **Windows Autopilot provisioning** option, and then select **Continue**.

    ![Windows Autopilot provisioning option.](../../images/choice.png)

1. In the **Windows Autopilot Configuration** screen, it displays the following information about the device:

   - The Autopilot profile assigned to the device.
   - The organization name for the device.
   - The user assigned to the device if a user was assigned in the **Assign Autopilot device to a user (optional)** step.
   - A QR code containing a unique identifier for the device. You can use this code to look up the device in Intune which you might want to do to verify configurations, and if make any necessary changes.

      > [!NOTE]
      >
      > The QR codes can be scanned using a companion app. The app also configures the device to specify who it belongs to. An [open-source sample of the companion app](https://github.com/Microsoft/WindowsAutopilotCompanion) that integrates with Intune by using the Graph API has been published to GitHub by the Autopilot team.

      ![Windows Autopilot configuration screen.](../../images/landing.png)

1. Validate that the information in the **Windows Autopilot Configuration** screen is correct. If any changes are needed, make the changes, and then select **Refresh** to redownload the updated Autopilot profile details.

1. Once all information has been confirmed as correct, select **Provision** to begin the provisioning process.

1. Once the provisioning process completes, a status screen will be displayed showing either success of failure:

   - If the pre-provisioning process completes successfully, a green status screen appears with information about the device, including the same details presented previously. For example, Autopilot profile, organization name, assigned user, and QR code. The elapsed time for the pre-provisioning steps is also provided.

        ![Green configuration screen.](../../images/white-glove-result.png)

     1. Select **Reseal** to shut down the device. At that point, the device can be shipped to the end user.

        > [!IMPORTANT]
        >
        > Outside of testing scenarios, if the intention is to deliver the device to an end user, **DON'T** turn the device back on at this point. Instead, deliver the device to the end user where they will perform the last step of [User flow](hybrid-azure-ad-join-user-flow.md).

        > [!NOTE]
        >
        > The technician flow inherits behavior from [self-deploying mode](../self-deploying/self-deploying-workflow.md). Self-deploying mode uses the Enrollment Status Page (ESP) to hold the device in a provisioning state and prevent the user from proceeding to the desktop after enrollment but before software and configuration is done applying. If the Enrollment Status Page (ESP) is disabled, the **Reseal** button may appear before software and configuration is done applying. This may advertently allow proceeding to the user flow before technician flow provisioning is complete. The green screen validates that enrollment was successful, not that the technician flow is necessarily complete. For this reason, it is strongly recommended not disable the Enrollment Status Page (ESP). Instead enable the Enrollment Status Page (ESP) as suggested in the [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md) step.

   - If the pre-provisioning process fails, a red status screen appears with information about the device, including the same details presented previously. The elapsed time for the pre-provisioning steps is also provided.

     - Diagnostic logs can be gathered from the device to troubleshoot the issue by selecting **View diagnostics**.

     - If the issue can be fixed, for example no network connectivity, then select the **Retry** button to retry provisioning the device

     - If the issue can't be immediately fixed or can't be fixed without a reset, then select the **Reset** button so that the process can be started over again.

## Next step: User flow

> [!div class="nextstepaction"]
> [Step 8: User flow](azure-ad-join-user-flow.md)

## More information

[!INCLUDE [More information technician flow](../includes/more-info-technician-flow.md)]
