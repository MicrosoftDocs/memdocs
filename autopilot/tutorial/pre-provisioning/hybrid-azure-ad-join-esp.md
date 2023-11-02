---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 6 of 11 - Configure and assign the Enrollment Status Page (ESP)
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 6 of 11 - Configure and assign the Enrollment Status Page (ESP).
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

# Pre-provision Microsoft Entra hybrid join: Configure and assign the Enrollment Status Page (ESP)

Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
> [!div class="checklist"]
> - **Step 6: Configure and assign Autopilot Enrollment Status Page (ESP)**
- Step 7: [Create and assign Microsoft Entra hybrid join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join overview](hybrid-azure-ad-join-workflow.md#workflow)

> [!NOTE]
>
> If you have already configured and assigned an ESP from another Autopilot scenario and want to keep the same settings for the ESP for the pre-provisioned Microsoft Entra hybrid join scenario, you can skip this step and move on to [Step 7: Create and assign Microsoft Entra hybrid join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md).

## The Enrollment Status Page (ESP)

[!INCLUDE [How to configure and assign an Enrollment Status Page (ESP) in Intune](../includes/configure-and-assign-esp.md)]

<a name='next-step-create-and-assign-pre-provisioned-hybrid-azure-ad-join-autopilot-profile'></a>

## Next step: Create and assign pre-provisioned Microsoft Entra hybrid join Autopilot profile

> [!div class="nextstepaction"]
> [Step 7: Create and assign Microsoft Entra hybrid join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)

## More information

[!INCLUDE [More information ESP](../includes/more-info-esp.md)]
