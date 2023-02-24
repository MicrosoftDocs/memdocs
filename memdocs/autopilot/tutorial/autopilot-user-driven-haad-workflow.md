---
title: Overview for Windows Autopilot user-driven hybrid Azure AD join in Intune
description: Overview for Windows Autopilot user-driven hybrid Azure AD join in Intune.
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

# Step by step tutorial for Windows Autopilot user-driven Azure AD join in Intune

*Applies to:*

- Windows 11
- Windows 10

## Windows Autopilot user-driven hybrid Azure AD join overview

This step by step tutorial will guide you through using Intune to perform a Windows Autopilot user-driven scenario when the devices are also joined to an on-premises domain, also known as hybrid Azure AD join.

The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot user-driven hybrid Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [Plan your hybrid Azure Active Directory join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan) to make sure all prerequisites are met for joining on-premises AD devices to Azure AD.

## Windows Autopilot user-driven hybrid Azure AD join workflow

Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign Autopilot profile > Verify hybrid Azure AD join

Autopilot user-driven Azure AD join steps:
> [!div class="checklist"]
> - Step 1: [Register devices as Autopilot devices](autopilot-user-driven-aadj-1-register-device.md)
> - Step 2: [Create a device group](autopilot-user-driven-aadj-2-create-device-group.md)
> - Step 3: [Configure and assign Autopilot Enrollment Status Page (ESP)](autopilot-user-driven-aadj-3-configure-and-assign-esp.md)
> - Step 4: [Create and assign Autopilot profile](autopilot-user-driven-aadj-4-create-and-assign-autopilot-profile.md)
> - Step 5: [Verify hybrid Azure AD join](/azure/active-directory/devices/howto-hybrid-join-verify)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## More info

- [Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](/mem/autopilot/windows-autopilot-hybrid)
