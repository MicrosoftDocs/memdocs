---
title: Overview for Windows Autopilot deployment for existing devices in Intune and Configuration Manager
description: Overview for Windows Autopilot deployment for existing devices in Intune and Configuration Manager.
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

# Step by step tutorial for Windows Autopilot deployment for existing devices in Intune and Configuration Manager

This step by step tutorial guides you through using Intune and Microsoft Configuration Manager to perform a Windows Autopilot deployment for existing devices.

The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot deployment for existing devices using Intune and Microsoft Configuration Manager. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment. This tutorial assumes familiarity with Microsoft Configuration Manager and that Microsoft Configuration Manager is already set up and configured to support operating system deployments.

## Workflow

Set up a Windows Autopilot deployment > Install required modules to obtain Autopilot profile(s) from Intune > Create JSON file for Autopilot profile(s) > Create package for JSON file in Configuration Manager > Distribute JSON package to distribution points in Configuration Manager > Create Autopilot task sequence in Configuration Manager > Create collection in Configuration Manager > Deploy Autopilot task sequence to collection in Configuration Manager > Speed up the deployment process (optional) > Run Autopilot task sequence on device > Register device for Windows Autopilot

Autopilot user-driven Azure AD join steps:
> [!div class="checklist"]
> - Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
> - Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
> - Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
> - Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
> - Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
> - Step 6: [Create collection in Configuration Manager](create-collection.md)
> - Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
> - Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
> - Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
> - Step 10: [Register device for Windows Autopilot](register-device.md)

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)

## More information

For more information on Windows Autopilot deployment for existing devices, see the following article(s):

- [Windows Autopilot deployment for existing devices](/mem/autopilot/existing-devices)
