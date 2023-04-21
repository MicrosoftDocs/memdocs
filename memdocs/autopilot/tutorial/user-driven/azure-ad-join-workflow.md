---
title: Overview for Windows Autopilot user-driven Azure AD join in Intune
description: Overview for Windows Autopilot user-driven Azure AD join in Intune.
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

# Step by step tutorial for Windows Autopilot user-driven Azure AD join in Intune

This step by step tutorial guides you through using Intune to perform a Windows Autopilot user-driven scenario when the devices are strictly Azure AD joined.

The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot user-driven Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Windows Autopilot user-driven Azure AD join overview

Windows Autopilot user-driven Azure AD join is an Autopilot solution that automates the configuration of Windows on a new device delivered directly from an OEM or reseller without the need for IT intervention. Windows Autopilot user-driven deployments use the existing Windows installation installed by the OEM at the factory. The end-user only needs to perform a minimal number of actions during the deployment process such as:

- Powering on the device.
- In certain scenarios, selecting the language, locale, and keyboard layout.
- Connecting to a wireless network if the device isn't connected to a wired network.
- Signing into Azure AD with the end-user's Azure AD credentials.

Windows Autopilot user-driven deployments can perform the following tasks during the deployment:

- Joins the device to Azure AD.
- Enrolls the device in Intune.
- Installs applications.
- Applies device configuration policies such as BitLocker and Windows Hello for Business.
- Checks for compliance.
- Enrollment Status Page (ESP) can be used to prevent an end-user from using the device until it's fully configured.

Windows Autopilot user-driven deployments consist of two phases:

- Device ESP phase: Windows is configured and applications and policies assigned to the device are applied.
- User ESP phase: Applications and policies assigned to the user are applied.

Once the Windows Autopilot user-driven deployment is complete, the device is ready for the end-user to use and they're immediately sent to the Desktop.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot user-driven Azure AD join in Intune:

Set up Windows automatic Intune enrollment > Allow users to join devices to Azure AD > Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign Autopilot profile > Assign Autopilot device to a user (optional) > Deploy device to end-user

Autopilot user-driven Azure AD join steps:
> [!div class="checklist"]
> - Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
> - Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
> - Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
> - Step 4: [Create a device group](azure-ad-join-device-group.md)
> - Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
> - Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
> - Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)

## More information

For more information on Windows Autopilot user-driven Azure AD join, see the following article(s):

- [User-driven mode for Azure AD join](/mem/autopilot/user-driven#user-driven-mode-for-azure-ad-join)
