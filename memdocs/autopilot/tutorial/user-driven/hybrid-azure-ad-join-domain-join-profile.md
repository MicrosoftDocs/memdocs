---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 8 of 9 - Create and assign a domain join profile
description: How to - Windows Autopilot user-driven hybrid Azure AD join - Step 8 of 9 - Create and assign a domain join profile.
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

# User-driven hybrid Azure AD join: Create and assign a domain join profile

Autopilot user-driven hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
> [!div class="checklist"]
> - **Step 8: Configure and assign domain join profile**
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)

For an overview of the Windows Autopilot user-driven hybrid Azure AD join workflow, see [Windows Autopilot user-driven hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

> [!NOTE]
>
> If you've already created a domain join profile as part of the [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join](../pre-provisioning/hybrid-azure-ad-join-domain-join-profile.md) scenario and want to keep the same settings and assignments, you can move on to the [Next step: Assign Autopilot device to a user (optional)](#next-step-assign-autopilot-device-to-a-user-optional) section.

## Create and assign a domain join profile

[!INCLUDE [Create and assign a domain join profile](../includes/domain-join-profile.md)

## Next step: Assign Autopilot device to a user (optional)

> [!div class="nextstepaction"]
> [Step 7: Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)

> [!NOTE]
>
> If you don't plan to assign a user to the device, at this point, the device is ready to be deployed. If desired, deploy any additional applications, policies, and profiles that should run during Autopilot to the device group that the device is a member of. Boot the device with a fresh install of Windows and the Autopilot deployment should begin.

## More information

For more information on domain join profiles, see the following article(s):

- [Create and assign a Domain Join profile](/mem/autopilot/windows-autopilot-hybrid#create-and-assign-a-domain-join-profile)
