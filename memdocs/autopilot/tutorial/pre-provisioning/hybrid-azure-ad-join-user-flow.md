---
title: Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 10 of 10 - User flow
description: How to - Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 10 of 10 - User flow.
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

# Pre-provisioning hybrid Azure AD join: User flow

Windows Autopilot for pre-provisioned deployment hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector (OU)](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
> [!div class="checklist"]
> - **Step 10: User flow**

For an overview of the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

## User flow

Once the pre-provisioning process completes successfully and the device was resealed, the device can be delivered to the end-user. The end-user then completes the normal Windows Autopilot user-driven process. This final step is know as the user flow and involves the following steps:

1. If a wired network connection is available, connect the device to the network.

1. Power on the device.

1. Select the appropriate language, locale, and keyboard layout.

1. If not connected to a wired network, a screen will prompt to connect to a Wi-Fi network. Connect to a Wi-Fi network. Internet access is always required and there must also be connectivity to a domain controller.

1. The device will reboot. After the reboot, the end-user's Active Directory credentials need to be entered.

At this point, any policies and apps assigned to the user are delivered to the device and are tracked by the Enrollment Status Page (ESP). Once complete, the user can access the desktop.

> [!NOTE]
>
> Although device ESP ran during the [Technician flow](hybrid-azure-ad-join-technician-flow.md), during the user flow when the end-user logs in, the device ESP will rerun again . This allows ESP to install other policies that may have been assigned to the device after it was provisioned in the technician flow.

## More information

[!INCLUDE [More information user flow](../includes/more-info-user-flow.md)]
