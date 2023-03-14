---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 5 of 8 - Create a device group
description: How to - Windows Autopilot hybrid user-driven Azure AD join - Step 5 of 8 - Create a device group.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/14/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# User-driven hybrid Azure AD join: Create a device group

Autopilot user-driven hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
> [!div class="checklist"]
> - **Step 5: Create a device group**
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)

For an overview of the Windows Autopilot user-driven hybrid Azure AD join workflow, see [Windows Autopilot user-driven hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

> [!NOTE]
>
> If you've already created device groups from another Autopilot scenario, you can skip this step and move on to [Step 6: Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md). However, be aware that if you're deploying multiple different Autopilot scenarios to different devices, separate device groups will be required for each Autopilot scenario.

## Create a device group

[!INCLUDE [How to create a device group in Intune](../includes/create-device-group.md)]

## Next step: Configure and assign the Enrollment Status Page (ESP)

> [!div class="nextstepaction"]
> [Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)

## More information

[!INCLUDE [More information device group](../includes/more-info-device-group.md)]
