---
title: Overview for Windows Autopilot user-driven Azure AD join in Intune
description: Overview for Windows Autopilot user-driven Azure AD join in Intune.
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

## Windows Autopilot user-driven Azure AD join overview

This step by step tutorial will guide you through using Intune to perform a Windows Autopilot user-driven scenario when the devices will be strictly Azure AD joined.

The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot user-driven Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Windows Autopilot user-driven Azure AD join workflow

Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign Autopilot profile> Assign Autopilot device to a user (optional)

Autopilot user-driven Azure AD join steps:
> [!div class="checklist"]
> - Step 1: [Set up Windows automatic enrollment](azure-ad-join-automatic-enrollment.md)
> - Step 2: [Configure device settings](azure-ad-join-device-settings.md)
> - Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
> - Step 4: [Create a device group](azure-ad-join-device-group.md)
> - Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
> - Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
> - Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## Step 1 of 7: Set up Windows automatic enrollment

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic enrollment](azure-ad-join-automatic-enrollment.md)

## More info

- [Windows Autopilot user-driven mode](/mem/autopilot/user-driven)
