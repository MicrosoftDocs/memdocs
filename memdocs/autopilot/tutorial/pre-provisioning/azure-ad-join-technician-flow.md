---
title: Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - Technician flow
description: How to - Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - Technician flow.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision Azure AD join: Technician flow

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
- Step 9: [User flow](azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment Azure AD join overview](azure-ad-join-workflow.md#workflow)

## Technician flow

[!INCLUDE [Technician flow](../includes/technician-flow.md)]

## Technician flow tips

- Before starting the Autopilot deployment, you may want to have:

  - At least one type of policy and at least one application assigned to the device(s).
  - At least one type of policy and at least one application assigned to the user(s).

    These assignments ensure proper testing of the Autopilot deployment during both the Device ESP phase and User ESP phase of the ESP. It may also prevent possible issues when there are either no policies or no applications assigned to the device(s) or the user(s).

- Depending on how the Autopilot profile was configured at the [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md) step, additional screens may appear during the Autopilot deployment before the Azure AD sign-in page such as:

  - Language/Country/Region.
  - Keyboard.
  - License Terms.

- The QR codes can be scanned using a companion app. The app can be used to assign a user to the device. The Autopilot team has published to GitHub an [open-source sample of the companion app](https://github.com/Microsoft/WindowsAutopilotCompanion) that integrates with Intune using the Graph API.

- To view and hide detailed progress information in the ESP during the provisioning process:

  - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
  - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

- The technician flow inherits behavior from [self-deploying mode](../self-deploying/self-deploying-workflow.md). Self-deploying mode uses the Enrollment Status Page (ESP) to hold the device in a provisioning state and prevent the user from proceeding to the desktop after enrollment but before applications and configurations are done applying. If the Enrollment Status Page (ESP) is disabled, the **Reseal** button may appear before applications and configurations are done applying. Disabling the ESP may advertently allow proceeding to the user flow before technician flow provisioning is complete. The success status screen validates that enrollment was successful, not that the technician flow is necessarily complete. For this reason, it's recommended not to disable the Enrollment Status Page (ESP). Instead enable the Enrollment Status Page (ESP) as suggested in the **Configure and assign Autopilot Enrollment Status Page (ESP)** step.

## Next step: User flow

> [!div class="nextstepaction"]
> [Step 8: User flow](azure-ad-join-user-flow.md)

## More information

[!INCLUDE [More information technician flow](../includes/more-info-technician-flow.md)]
