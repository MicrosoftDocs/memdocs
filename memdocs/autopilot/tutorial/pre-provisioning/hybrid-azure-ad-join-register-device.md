---
title: Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 4 of 10 - Register devices as Autopilot devices
description: How to - Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 4 of 10 - Register devices as Autopilot devices.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/27/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Pre-provisioning hybrid Azure AD join: Register devices as Autopilot devices

Windows Autopilot for pre-provisioned deployment hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector (OU)](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit](hybrid-azure-ad-join-computer-account-limit.md)
> [!div class="checklist"]
> - **Step 4: Register devices as Autopilot devices**
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Technician phase](hybrid-azure-ad-join-technician-phase.md)
- Step 10: [User phase](hybrid-azure-ad-join-user-phase.md)

For an overview of the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

> [!NOTE]
>
> If you've already registered devices as Autopilot devices from another Autopilot scenario, you can skip this step and move on to [Step 5: Create a device group](hybrid-azure-ad-join-device-group.md). However, be aware that if you're deploying multiple different Autopilot scenarios to different devices, separate device groups will be required for each Autopilot scenario.

## Register devices as Autopilot devices

[!INCLUDE [How to register a device as an Autopilot device in Intune](../includes/register-autopilot-device.md)]

## Next step: Create a device group

> [!div class="nextstepaction"]
> [Step 5: Create a device group](hybrid-azure-ad-join-device-group.md)

## More information

[!INCLUDE [More information register Autopilot device](../includes/more-info-register-device.md)]
