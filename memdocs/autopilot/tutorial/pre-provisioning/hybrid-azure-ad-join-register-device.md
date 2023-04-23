---
title: Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 4 of 11 - Register devices as Autopilot devices
description: How to - Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 4 of 11 - Register devices as Autopilot devices.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/11/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision hybrid Azure AD join: Register devices as Autopilot devices

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
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md#workflow)

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
