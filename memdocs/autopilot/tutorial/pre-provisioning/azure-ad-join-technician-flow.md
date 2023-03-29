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

- Boot the device.
- From the first OOBE screen (which could be a language selection, locale selection screen, or the Azure AD sign-in page), don't select **Next**. Instead, press the Windows key five times to view another options dialog. From that screen, choose the **Windows Autopilot provisioning** option and then select **Continue**.


 ![Windows Autopilot provisioning option.](images/choice.png)

- On the **Windows Autopilot Configuration** screen, it displays the following information about the device:
  - The Autopilot profile assigned to the device.
  - The organization name for the device.
  - The user assigned to the device (if there's one).
  - A QR code containing a unique identifier for the device. You can use this code to look up the device in Intune, which you might want to do to make configuration changes. For example, assign a user or add the device to groups needed for app or policy targeting.

    > [!NOTE]
    > The QR codes can be scanned using a companion app. The app also configures the device to specify who it belongs to. An [open-source sample of the companion app](https://github.com/Microsoft/WindowsAutopilotCompanion) that integrates with Intune by using the Graph API has been published to GitHub by the Autopilot team.

- Validate the information displayed. If any changes are needed, make the changes, and then select **Refresh** to redownload the updated Autopilot profile details.

 ![Windows Autopilot configuration screen.](images/landing.png)

- Select **Provision** to begin the provisioning process.

If the pre-provisioning process completes successfully:

- A green status screen appears with information about the device, including the same details presented previously. For example, Autopilot profile, organization name, assigned user, and QR code. The elapsed time for the pre-provisioning steps is also provided.
 ![Green configuration screen.](images/white-glove-result.png)
- Select **Reseal** to shut down the device. At that point, the device can be shipped to the end user.

> [!NOTE]
> Technician flow inherits behavior from [self-deploying mode](self-deploying.md). Per the Self-Deploying Mode documentation, it uses the Enrollment Status Page to hold the device in a provisioning state and prevent the user from proceeding to the desktop after enrollment but before software and configuration is done applying. As such, if Enrollment Status Page is disabled, the reseal button may appear before software and configuration is done applying letting you proceed to the user flow before technician flow provisioning is complete. The green screen validates that enrollment was successful, not that the technician flow is necessarily complete.

If the pre-provisioning process fails:

- A red status screen appears with information about the device, including the same details presented previously. For example, Autopilot profile, organization name, assigned user, and QR code. The elapsed time for the pre-provisioning steps is also provided.
- Diagnostic logs can be gathered from the device, and then it can be reset to start the process over again.

## Next step: User flow

> [!div class="nextstepaction"]
> [Step 8: User flow](azure-ad-join-user-flow.md)

## More information

[!INCLUDE [More information technician flow](../includes/more-info-technician-flow.md)]
