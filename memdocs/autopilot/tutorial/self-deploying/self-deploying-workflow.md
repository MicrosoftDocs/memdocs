---
title: Overview for Windows self-deploying mode in Intune
description: Overview for Windows Autopilot self-deploying mode in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/09/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Step by step tutorial for Windows Autopilot self-deploying mode in Intune

*Applies to:*

- Windows 11
- Windows 10

This step by step tutorial will guide you through using Intune to perform a Windows Autopilot self-deploying mode scenario.

The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot self-deploying mode deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Workflow

Set up Windows automatic Intune enrollment > Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign Autopilot profile

Autopilot self-deploying mode steps:
> [!div class="checklist"]
> - Step 1: [Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)
> - Step 2: [Register devices as Autopilot devices](self-deploying-register-device.md)
> - Step 3: [Create a device group](self-deploying-device-group.md)
> - Step 4: [Configure and assign Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
> - Step 5: [Create and assign Autopilot profile](self-deploying-autopilot-profile.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)

## More information

For more information on Windows Autopilot self-deploying mode, see the following article(s):

- [Windows Autopilot self-deploying mode](/mem/autopilot/self-deploying)
