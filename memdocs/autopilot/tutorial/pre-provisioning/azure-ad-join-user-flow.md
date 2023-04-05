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

Once the pre-provisioning process completes successfully and the device was resealed, the device can be delivered to the end-user. The end-user then completes the normal Windows Autopilot user-driven process. This final step is know as the user flow and involves the following steps:

1. If a wired network connection is available, connect the device to the network.

1. Power on the device.

1. Select the appropriate language, locale, and keyboard layout.

1. If not connected to a wired network, a screen will prompt to connect to a Wi-Fi network. Connect to a Wi-Fi network. Internet access is always required.

1. On the branded sign-on screen, enter the user's Azure Active Directory credentials.

1. If using hybrid Azure AD Join, the device will reboot; after the reboot, enter the user's Active Directory credentials.

At this point, any policies and apps assigned to the user are delivered to the device and are tracked by the Enrollment Status Page (ESP). Once complete, the user can access the desktop.

> [!NOTE]
>
> Although device ESP ran during the [Technician flow](hybrid-azure-ad-join-technician-flow.md), during the user flow when the end-user logs in, the device ESP will rerun again . This allows ESP to install other policies that may have been assigned to the device after it was provisioned in the technician flow.

## More information

[!INCLUDE [More information user flow](../includes/more-info-user-flow.md)]
