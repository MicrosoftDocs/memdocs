---
title: Overview for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune
description: Overview for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/09/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Step by step tutorial for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune

This step by step tutorial guides you through using Intune to perform a Windows Autopilot device preparation user-driven scenario when the devices are Microsoft Entra joined.

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Windows Autopilot device preparation user-driven Microsoft Entra join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Microsoft Entra join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Microsoft Entra ID.

## Windows Autopilot user-driven Microsoft Entra join overview

Windows Autopilot device preparation user-driven Microsoft Entra join is a solution that automates the configuration of Windows on a new device without the need for IT intervention. Normally the device is delivered directly from an OEM or reseller to the end-user  Windows Autopilot device preparation user-driven deployments use the existing Windows installation installed by the OEM at the factory. The end-user only needs to perform a minimal number of actions during the deployment process such as:

- Powering on the device.
- In certain scenarios, selecting the language, locale, and keyboard layout.
- Connecting to a wireless network if the device isn't connected to a wired network.
- Signing into Microsoft Entra ID with the end-user's Microsoft Entra credentials.

Windows Autopilot device preparation user-driven deployments can perform the following tasks during the deployment:

- Joins the device to Microsoft Entra ID.
- Enrolls the device in Intune.
- Installs up to 10 critical applications.
- Runs up to 10 critical PowerShell scripts.

Once the Windows Autopilot device preparation user-driven deployment is complete, the device is ready for the end-user to use and they're immediately sent to the Desktop.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot device preparation user-driven Microsoft Entra join in Intune:

> [!div class="checklist"]
>
> - Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
> - Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
> - Step 3: [Create a device group](entra-join-device-group.md)
> - Step 4: [Create a user group](entra-join-user-group.md)
> - Step 5: [Assign applications and scripts to device group](entra-join-assign-apps-scripts.md)
> - Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
> - Step 7: [Identify device using corporate identifiers (optional)](entra-join-corporate-identifier.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)

## Related content
