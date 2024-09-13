---
title: Overview for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune
description: Overview for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 09/13/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Step by step tutorial for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune

This step by step tutorial guides through using Intune to perform a Windows Autopilot device preparation user-driven scenario when the devices are Microsoft Entra joined.

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Windows Autopilot device preparation user-driven Microsoft Entra join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Microsoft Entra join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all requirements are met for joining devices to Microsoft Entra ID.

## Windows Autopilot device preparation user-driven Microsoft Entra join overview

Windows Autopilot device preparation user-driven Microsoft Entra join is a solution that automates the configuration of Windows on a new device without the need for IT intervention. Normally the device is delivered directly from an OEM or reseller to the end-user  Windows Autopilot device preparation user-driven deployments use the existing Windows installation installed by the OEM at the factory. The end-user only needs to perform a minimal number of actions during the deployment process such as:

- Powering on the device.
- In certain scenarios, selecting the language, locale, and keyboard layout.
- Connecting to a wireless network if the device isn't connected to a wired network.
- Signing into Microsoft Entra ID with the end-user's Microsoft Entra credentials.

Windows Autopilot device preparation user-driven deployments can perform the following tasks during the deployment:

- Joins the device to Microsoft Entra ID.
- Enrolls the device in Intune.
- Installs up to 10 essential applications.
- Runs up to 10 essential PowerShell scripts.

Once the Windows Autopilot device preparation user-driven deployment is complete, the device is ready for the end-user to use and they're immediately sent to the desktop.

## Windows Autopilot device preparation user-driven Microsoft Entra join process

During the out-of-box experience (OOBE), a user authenticates with their corporate credentials. If there's a Windows Autopilot device preparation policy assigned to the user signing in, then that policy is delivered to the device. It then determines the configuration that needs to be applied to the device based on the settings configured in the policy. After that, device setup continues in the following order:

1. The device joins Microsoft Entra ID and enrolls in Intune.

1. The Intune management extension installs.

1. When the device is joined to Microsoft Entra ID during the first step, the user is automatically added to the local **Administrators** group on the device. If the user account is configured as a standard user, the setting is enforced by removing the user out of the **Administrators** group.

1. The deployment syncs with the mobile device management (MDM) service such as Intune and checks if line-of-business (LOB) and Microsoft 365 applications are selected in the Windows Autopilot device preparation policy. It also syncs all MDM policy at this time, but application of the policy isn't tracked during the deployment.

1. If there are LOB and Microsoft 365 applications selected in the policy, then they're installed. If a LOB or Microsoft 365 application fails to install, then the deployment fails at this point.

1. The deployment checks if PowerShell scripts are selected in the Windows Autopilot device preparation policy. If there are PowerShell scripts selected in the policy, then they run. If a PowerShell script fails, then the deployment fails at this point.

1. The deployment checks if Win32 and Microsoft Store applications are selected in the Windows Autopilot device preparation policy. If there are Win32 and Microsoft Store applications selected in the policy, then they're installed. If a Win32 or Microsoft Store application fails to install, then the deployment fails at this point.

1. If all steps succeed, the **Required setup complete** page is displayed for the user.

1. Once the **Required setup complete** page is dismissed, the user is automatically signed in and the desktop is displayed.

1. At this point, another sync is triggered and all other configurations is delivered to the device. Additional configurations might include:

    - Applications and PowerShell scripts that were assigned to the device group specified in the Windows Autopilot device preparation policy but weren't explicitly selected in the policy.
    - Any additional MDM policy.
    - User-based configurations.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot device preparation user-driven Microsoft Entra join in Intune:

> [!div class="checklist"]
>
> - Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
> - Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
> - Step 3: [Create a device group](entra-join-device-group.md)
> - Step 4: [Create a user group](entra-join-user-group.md)
> - Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
> - Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
> - Step 7: [Add Windows corporate identifier to device (optional)](entra-join-corporate-identifier.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
