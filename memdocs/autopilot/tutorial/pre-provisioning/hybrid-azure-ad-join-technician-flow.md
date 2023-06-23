---
title: Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 9 of 11 - Technician flow
description: How to - Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 9 of 11 - Technician flow.
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

# Pre-provision hybrid Azure AD join: Technician flow

Windows Autopilot for pre-provisioned deployment hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector (OU)](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
> [!div class="checklist"]
> - **Step 10: Technician flow**
- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md#workflow)

## Technician flow

> [!IMPORTANT]
>
> The technician flow portion of the hybrid Azure AD join process only requires connectivity to the Internet. It doesn't require connectivity to a domain controller. Connectivity to a domain controller to perform an on-premises domain join isn't needed until the next step of [User flow](hybrid-azure-ad-join-user-flow.md) is run.

[!INCLUDE [Technician flow](../includes/technician-flow.md)]

## Technician flow tips

- Before starting the Autopilot deployment, you may want to have:

  - At least one type of policy and at least one application assigned to the device(s).
  - At least one type of policy and at least one application assigned to the user(s).

    These assignments ensure proper testing of the Autopilot deployment during both the Device ESP phase and User ESP phase of the ESP. It may also prevent possible issues when there are either no policies or no applications assigned to the device(s) or the user(s).

- Depending on how the Autopilot profile was configured at the [Create and assign Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md) step, additional screens may appear during the Autopilot deployment before the Azure AD sign-in page such as:

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
> [Step 11: User flow](hybrid-azure-ad-join-user-flow.md)

## More information

[!INCLUDE [More information technician flow](../includes/more-info-technician-flow.md)]
