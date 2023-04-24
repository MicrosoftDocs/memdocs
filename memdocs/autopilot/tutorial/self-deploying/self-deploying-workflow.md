---
title: Overview for Windows Autopilot self-deploying mode in Intune
description: Overview for Windows Autopilot self-deploying mode in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Step by step tutorial for Windows Autopilot self-deploying mode in Intune

This step by step tutorial guides you through using Intune to perform a Windows Autopilot self-deploying mode scenario.

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Autopilot self-deploying mode deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Windows Autopilot self-deploying mode overview

Windows Autopilot self-deploying mode is an Autopilot solution that automates the configuration of Windows on a new device delivered directly from an IT department, OEM, or reseller. Windows Autopilot for pre-provisioned deployment uses the existing Windows installation installed by the OEM at the factory. Windows Autopilot self-deploying mode is designed for kiosk like devices or devices shared by multiple users. For this reason, Windows Autopilot self-deploying mode doesn't support assigning users to the device. Additionally, Windows Autopilot self-deploying mode only supports Azure AD join. It doesn't support hybrid Azure AD join.

The main advantage of Windows Autopilot self-deploying mode over other Autopilot deployments methods is that it minimizes the interaction needed during the initial deployment of the device. Interactions are minimized because there's no single user assigned to the device. After first powering on the device, usually the only interactions needed, if any, are:

- In certain scenarios, selecting the language, locale, and keyboard layout.
- Connecting to a wireless network if the device isn't connected to a wired network.

In certain scenarios after first turning on the device, such as when the device is on a wired network connection, zero interaction may be possible.

Windows Autopilot self-deploying mode can perform the following tasks during the deployment:

- Joins the device to Azure AD.
- Enrolls the device in Intune.
- Installs applications.
- Applies device configuration policies such as BitLocker and Windows Hello for Business.
- Checks for compliance.

Once the Windows Autopilot self-deploying mode is complete, the device goes to the Windows sign-on screen and is ready for use. Any end-user signing into the device needs to sign on with their Azure AD credentials. For devices such as kiosks, it's also possible to configure Intune policies that automatically sign a user into the device.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot self-deploying mode in Intune:

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
