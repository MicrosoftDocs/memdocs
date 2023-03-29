---
title: Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 6 of 10 - Configure and assign the Enrollment Status Page (ESP)
description: How to - Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 6 of 10 - Configure and assign the Enrollment Status Page (ESP).
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

# Pre-provisioning hybrid Azure AD join: Configure and assign the Enrollment Status Page (ESP)

Windows Autopilot for pre-provisioned deployment hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
> [!div class="checklist"]
> - **Step 6: Configure and assign Autopilot Enrollment Status Page (ESP)**
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Technician phase](hybrid-azure-ad-join-technician-phase.md)
- Step 10: [User phase](hybrid-azure-ad-join-user-phase.md)

For an overview of the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

> [!NOTE]
>
> If you've already configured and assigned an ESP from another Autopilot scenario and want to keep the same settings for the ESP for the pre-provisioned hybrid Azure AD join scenario, you can skip this step and move on to [Step 7: Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md).

## Configure and assign the Enrollment Status Page (ESP)

[!INCLUDE [How to configure and assign an Enrollment Status Page (ESP) in Intune](../includes/configure-and-assign-esp.md)]

## Next step: Create and assign pre-provisioned hybrid Azure AD join Autopilot profile

> [!div class="nextstepaction"]
> [Step 7: Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)

## More information

[!INCLUDE [More information ESP](../includes/more-info-esp.md)]
