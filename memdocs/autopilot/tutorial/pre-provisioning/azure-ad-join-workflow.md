---
title: Overview for Windows Autopilot for pre-provisioned deployment Azure AD join with pre-provisioning in Intune
description: Overview for Windows Autopilot for pre-provisioned deployment Azure AD join with pre-provisioning in Intune.
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

# Step by step tutorial for Windows Autopilot for pre-provisioned deployment Azure AD join in Intune

This step by step tutorial guides you through using Intune to perform a Windows Autopilot for pre-provisioned deployment scenario when the devices are strictly Azure AD joined.

The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot for pre-provisioned deployment Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

> [!NOTE]
>
> Since Windows Autopilot for pre-provisioned deployment Azure AD join builds on top of [Windows Autopilot user-driven Azure AD join](../user-driven/azure-ad-join-workflow.md), it's strongly recommended that the Windows Autopilot user-driven Azure AD join scenario is setup, tested, and working first before attempting to use the Windows Autopilot for pre-provisioned deployment Azure AD join scenario. If the Windows Autopilot user-driven Azure AD join doesn't work, then most likely the Windows Autopilot pre-provisioned deployment Azure AD join scenario won't work either.

## Workflow

Set up Windows automatic Intune enrollment > Allow users to join devices to Azure AD > Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign Autopilot profile > Assign Autopilot device to a user (optional) > Technician flow > User flow

Windows Autopilot for pre-provisioned deployment Azure AD join steps:
> [!div class="checklist"]
> - Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
> - Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
> - Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
> - Step 4: [Create a device group](azure-ad-join-device-group.md)
> - Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
> - Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
> - Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
> - Step 8: [Technician flow](azure-ad-join-technician-flow.md)
> - Step 9: [User flow](azure-ad-join-user-flow.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)

## More information

For more information on Windows Autopilot for pre-provisioned deployment Azure AD join, see the following article(s):

- [Windows Autopilot for pre-provisioned deployment](/mem/autopilot/pre-provision)
- [User-driven mode for Azure AD join](/mem/autopilot/user-driven#user-driven-mode-for-azure-ad-join)
