---
title: Overview for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune
description: Overview for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune.
ms.date: 08/07/2026
ms.topic: tutorial
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Step by step tutorial for Windows Autopilot device preparation user-driven Microsoft Entra join in Intune

This step by step tutorial guides through using Intune to perform a Windows Autopilot device preparation user-driven scenario when the devices are Microsoft Entra joined.

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Windows Autopilot device preparation user-driven Microsoft Entra join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to [Plan your Microsoft Entra device deployment](/entra/identity/devices/device-join-plan) to make sure all requirements are met for joining devices to Microsoft Entra ID.

## Windows Autopilot device preparation user-driven Microsoft Entra join overview

Windows Autopilot device preparation user-driven Microsoft Entra join is a solution that automates the configuration of Windows on a new device without the need for IT intervention. Normally the device is delivered directly from an OEM or reseller to the end-user. Windows Autopilot device preparation user-driven deployments use the existing Windows installation installed by the OEM at the factory. The end-user only needs to perform a minimal number of actions during the deployment process such as:

- Powering on the device.
- In certain scenarios, selecting the language, locale, and keyboard layout.
- Connecting to a wireless network if the device isn't connected to a wired network.
- Signing in to Microsoft Entra ID with the end-user's Microsoft Entra credentials.

Windows Autopilot device preparation user-driven deployments can perform the following tasks during the deployment:

- Joins the device to Microsoft Entra ID.
- Enrolls the device in Intune.
- Installs up to 25 essential applications.
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

1. The deployment checks if Win32, Microsoft Store, or Enterprise App Catalog applications are selected in the Windows Autopilot device preparation policy. If there are Win32, Microsoft Store, or Enterprise App Catalog applications selected in the policy, then they're installed. If a Win32, Microsoft Store, or Enterprise App Catalog application fails to install, then the deployment fails at this point.

1. If all steps succeed, the **Required setup complete** page is displayed for the user.

1. Once the **Required setup complete** page is dismissed, the user is automatically signed in and the desktop is displayed.

1. At this point, another sync is triggered and all other configurations is delivered to the device. Additional configurations might include:

    - Applications and PowerShell scripts that were assigned to the device group specified in the Windows Autopilot device preparation policy but weren't explicitly selected in the policy.
    - Any additional MDM policy.
    - User-based configurations.

## Workflow

Steps 1–6 configure your environment and the Windows Autopilot device preparation policy. They're required for all deployments:

> [!div class="checklist"]
>
> - Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
> - Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
> - Step 3: [Create an assigned device group](entra-join-device-group.md)
> - Step 4: [Create a user group](entra-join-user-group.md)
> - Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)
> - Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)

### Step 7 (optional): Make sure only trusted devices are onboarded

If you use Intune enrollment restrictions to block personal device enrollments, you must configure **either** corporate identifiers **or** device association for each device before deployment. You don't need both. If a device is associated, you don't need to upload a corporate identifier for it. If personal devices aren't blocked in your environment, you can skip this step and deploy the device.

Choose one of the following options:

> [!div class="checklist"]
>
> - Step 7, option 1: [Add Windows corporate identifier to device](entra-join-corporate-identifier.md)
> - Step 7, option 2: [Associate devices](entra-join-device-association.md)

Device association also unlocks additional device preparation policy settings—such as OOBE customization and device naming—that are only available to associated devices.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
