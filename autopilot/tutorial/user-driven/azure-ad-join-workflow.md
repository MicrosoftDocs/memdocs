---
title: Overview for Windows Autopilot user-driven Microsoft Entra join in Intune
description: Overview for Windows Autopilot user-driven Microsoft Entra join in Intune.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Step by step tutorial for Windows Autopilot user-driven Microsoft Entra join in Intune

This step by step tutorial guides through using Intune to perform a Windows Autopilot user-driven scenario when the devices are strictly Microsoft Entra joined.

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Autopilot user-driven Microsoft Entra join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Microsoft Entra join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all requirements are met for joining devices to Microsoft Entra ID.

## Windows Autopilot user-driven Microsoft Entra join overview

Windows Autopilot user-driven Microsoft Entra join is an Autopilot solution that automates the configuration of Windows on a new device. Normally, the device is delivered directly from an OEM or reseller to the end-user without the need for IT intervention. Windows Autopilot user-driven deployments use the existing Windows installation installed by the OEM at the factory. The end-user only needs to perform a minimal number of actions during the deployment process such as:

- Powering on the device.
- In certain scenarios, selecting the language, locale, and keyboard layout.
- Connecting to a wireless network if the device isn't connected to a wired network.
- Signing into Microsoft Entra ID with the end-user's Microsoft Entra credentials.

Windows Autopilot user-driven deployments can perform the following tasks during the deployment:

- Joins the device to Microsoft Entra ID.
- Enrolls the device in Intune.
- Installs applications.
- Applies device configuration policies such as BitLocker and Windows Hello for Business.
- Checks for compliance.
- Enrollment Status Page (ESP) can be used to prevent an end-user from using the device until it's fully configured.

Windows Autopilot user-driven deployments consist of two phases:

- Device ESP phase: Windows is configured and applications and policies assigned to the device are applied.
- User ESP phase: Applications and policies assigned to the user are applied.

Once the Windows Autopilot user-driven deployment is complete, the device is ready for the end-user to use and they're immediately sent to the desktop.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot user-driven Microsoft Entra join in Intune:

> [!div class="checklist"]
>
> - Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
> - Step 2: [Allow users to join devices to Microsoft Entra ID](azure-ad-join-allow-users-to-join.md)
> - Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
> - Step 4: [Create a device group](azure-ad-join-device-group.md)
> - Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
> - Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
> - Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
> - Step 8: [Deploy the device](azure-ad-join-deploy-device.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps might make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step might make more sense in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)

## Related content

For more information on Windows Autopilot user-driven Microsoft Entra join, see the following article:

- [User-driven mode for Microsoft Entra join](../../user-driven.md#user-driven-mode-for-microsoft-entra-join).
