---
title: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune
description: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune.
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

# Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune

*Applies to:*

- Windows 11
- Windows 10

## Windows Autopilot user-driven Azure AD join mode overview

This step by step tutorial will guide you through using Intune to perform a Windows Autopilot user-driven scenario when the devices will be strictly Azure AD joined. The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot user-driven Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Windows Autopilot user-driven Azure AD join mode workflow

Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign Autopilot profile> Assign Autopilot device to a user (optional)

1. [Register devices as Autopilot devices](autopilot-user-driven-aadj-1-register-device.md)
2. [Create a device group](autopilot-user-driven-aadj-2-create-device-group.md)
3. [Configure and assign Autopilot Enrollment Status Page (ESP)](autopilot-user-driven-aadj-3-configure-and-assign-esp.md)
4. [Create and assign Autopilot profile](autopilot-user-driven-aadj-4-create-and-assign-autopilot-profile.md)
5. [Assign Autopilot device to a user (optional)](autopilot-user-driven-aadj-5-assign-autopilot-device-to-user.md)

> [!NOTE]
>
> The workflow is designed for lab or testing scenarios. However, some of the steps in the workflow are interchangeable. A workflow with some of these steps interchanged may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## More info

- [Windows Autopilot user-driven mode](/mem/autopilot/user-driven)
