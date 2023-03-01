---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 5 of 8 - Create a device group
description: How to - Windows Autopilot hybrid user-driven Azure AD join - Step 5 of 8 - Create a device group.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/13/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# User-driven hybrid Azure AD join: Create a device group

Autopilot user-driven hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Increase the computer account limit in the Organizational Unit](hybrid-azure-ad-join-computer-account-limit.md)
- Step 3: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
> [!div class="checklist"]
> - **Step 5: Create a device group**
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)

For an overview of the Windows Autopilot hybrid user-driven Azure AD join workflow, see [Windows Autopilot user-driven hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

## Create a device group

[!INCLUDE [How to create a device group in Intune](../includes/create-device-group.md)]

## Next step - Step 5 of 8: Configure and assign the Enrollment Status Page (ESP)

> [!div class="nextstepaction"]
> [Step 5: Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)

## More information

For more information on creating groups in Intune, see the following articles:

- [Create device groups](/mem/autopilot/enrollment-autopilot)
- [Add groups to organize users and devices](/mem/intune/fundamentals/groups-add)
- [Manage Azure Active Directory groups and group membership](/azure/active-directory/fundamentals/how-to-manage-groups)
