---
title: Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - User flow
description: How to - Windows Autopilot for pre-provisioned deployment Azure AD join - Step 8 of 9 - User flow.
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

If the pre-provisioning process completed successfully and the device was resealed, you can deliver to the end user. The end user completes the normal Windows Autopilot user-driven process following these steps:

- Power on the device.
- Select the appropriate language, locale, and keyboard layout.
- Connect to a network (if using Wi-Fi). Internet access is always required. If using hybrid Azure AD Join, there must also be connectivity to a domain controller.
- If using Azure AD join, on the branded sign-on screen, enter the user's Azure Active Directory credentials.
- If using hybrid Azure AD Join, the device will reboot; after the reboot, enter the user's Active Directory credentials.
- More policies and apps are delivered to the device, as tracked by the Enrollment Status Page (ESP). Once complete, the user can access the desktop.

A change was made in the 2021.09C release to rerun the device ESP during the user flow so that both device and user ESP run when the user logs in. This change allows ESP to install other policies that may have been assigned to the device after it was provisioned in the technician flow.  

> [!NOTE]
> If the Microsoft Account Sign-In Assistant (wlidsvc) is disabled during the Technician Flow, the Azure AD sign in option may not show. Instead, users are asked to accept the EULA, and create a local account, which may not be what you want.

## More information

[!INCLUDE [More information user flow](../includes/more-info-user-flow.md)]
