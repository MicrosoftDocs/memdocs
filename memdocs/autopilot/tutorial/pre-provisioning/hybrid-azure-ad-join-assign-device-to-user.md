---
title: Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 9 of 11 - Assign Autopilot device to a user
description: How to - Windows Autopilot for pre-provisioned deployment hybrid Azure AD join with pre-provisioning - Step 9 of 11 - Assign Autopilot device to a user.
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

# Pre-provision hybrid Azure AD join: Assign Autopilot device to a user (optional)

Windows Autopilot for pre-provisioned deployment hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector (OU)](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
> [!div class="checklist"]
> - **Step 9: Assign Autopilot device to a user (optional)**
- Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md#workflow)

## Assign Autopilot device to a user (optional)

[!INCLUDE [How to assign an Autopilot device to a user](../includes/assign-autopilot-device-to-user.md)]

## Assigning Autopilot device to a user via hardware hash CSV file

[!INCLUDE [How to assign an Autopilot device to a user via hardware hash CSV file](../includes/assign-autopilot-device-to-user-via-csv.md)]

## Next step: Technician flow

> [!div class="nextstepaction"]
> [Step 10: Technician flow](hybrid-azure-ad-join-technician-flow.md)

## More information

For more information on assigning a user to an Autopilot device, see the following article(s):

- [Assign a user to a specific Autopilot device](/mem/autopilot/enrollment-autopilot#assign-a-user-to-a-specific-autopilot-device)
