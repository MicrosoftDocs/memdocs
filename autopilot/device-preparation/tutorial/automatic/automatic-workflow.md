---
title: Overview for Windows Autopilot device preparation in automatic mode for Windows 365 (preview) in Intune
description: Overview for Windows Autopilot device preparation in automatic mode for Windows 365 (preview) in Intune.
ms.date: 11/21/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Step by step tutorial for Windows Autopilot device preparation in automatic mode for Windows 365 (preview) in Intune  

> [!NOTE]
> This feature is in public preview.  

This step by step tutorial guides through using Intune to perform a Windows Autopilot device preparation in automatic mode for Windows 365. You can use Windows Autopilot device preparation policies in automatic mode to provision these supported SKUs:  

- Windows 365 Frontline in shared mode  
- Windows 365 Enterprise  
- Windows 365 Frontline in dedicated mode  
- Windows 365 Cloud Apps  

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Windows Autopilot device preparation in automatic mode for Windows 365 deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Microsoft Entra join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all requirements are met for joining devices to Microsoft Entra ID.

## Windows Autopilot device preparation in automatic mode for Windows 365 (preview) overview

Windows Autopilot device preparation in automatic mode for Windows 365 (preview), also known as Windows Autopilot device preparation automatic mode, is a solution that adds an additional Windows Autopilot device preparation policy that can be included in Windows 365 provisioning policies. By including the Windows Autopilot device preparation policy in the Windows 365 provisioning policies, it ensures that essential required device-targeted apps and scripts in Intune are installed on Cloud PCs during the provisioning process before the user signs in. This feature helps increase standardization of Cloud PCs while reducing the management overhead that comes with IT admins creating and managing their own custom images with pre-installed applications.

Windows Autopilot device preparation tracks the installation progress of specified Intune applications and scripts during Cloud PC provisioning. Instead of marking Cloud PCs as **Provisioned** after Intune enrollment, Windows Autopilot device preparation and Windows 365 wait until those workloads are fully installed. IT admins see a new status of **Preparing** reflected in the console while Windows Autopilot device preparation is underway.

## Windows Autopilot device preparation in automatic mode for Windows 365 (preview) process

1. The Windows 365 Cloud PC agent creates the Cloud PC.

1. Once the Cloud PC is created, the Cloud PC agent joins Microsoft Entra.

1. The Cloud PC agent triggers Intune enrollment.

1. The Cloud PC agent calls the Windows Autopilot device preparation policy assigned to the Cloud PC provisioning policy and the configuration is applied including:

   1. The Intune management extension is installed.

   1. The deployment syncs with Intune and checks if line-of-business (LOB) and Microsoft 365 applications are selected in the Windows Autopilot device preparation policy. It also syncs all MDM policy at this time, but application of the policy isn't tracked during the deployment. If this step fails, the **Deployment Status** shows up as **Failed** during the phase **Policy installation** in the [Windows Autopilot device preparation reporting and monitoring](../../reporting-monitoring.md).

   1. If there are LOB and Microsoft 365 applications selected in the policy, then they're installed. If any application installation fails, the **Deployment Status** shows up as **Failed** during the phase **Apps installation** in the [Windows Autopilot device preparation reporting and monitoring](../../reporting-monitoring.md).

   1. The deployment checks if PowerShell scripts are selected in the Windows Autopilot device preparation policy. If there are PowerShell scripts selected in the policy, then they run. If any script fails, the **Deployment Status** shows up as **Failed** during the phase **Scripts installation** in the [Windows Autopilot device preparation reporting and monitoring](../../reporting-monitoring.md).

   1. The deployment checks if Win32, Microsoft Store, or Enterprise App Catalog applications are selected in the Windows Autopilot device preparation policy. If there are Win32, Microsoft Store, or Enterprise App Catalog applications selected in the policy, then they're installed. If any application installation fails, the **Deployment Status** shows up as **Failed** during the phase **Apps installation** in the [Windows Autopilot device preparation reporting and monitoring](../../reporting-monitoring.md).

    > [!IMPORTANT]
    >
    > As part of a Windows Autopilot device preparation in automatic mode for Windows 365 deployment:
    >
    > - Up to 10 essential applications can be installed.
    > - Up to 10 essential PowerShell scripts can be run.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot device preparation in automatic mode for Windows 365 in Intune:

> [!div class="checklist"]
>
> - Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)
> - Step 2: [Create an assigned device group](automatic-device-group.md)
> - Step 3: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
> - Step 4: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)
> - Step 5: [Create a Cloud PC provisioning policy](automatic-cloud-pc-provisioning-policy.md)
> - Step 6: [Monitor the deployment](automatic-monitor.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)

## Related articles

- [Windows 365 Frontline Cloud PC in shared mode - Quick Start Guide](https://techcommunity.microsoft.com/discussions/windows365discussions/windows-365-frontline-cloud-pc-in-shared-mode-%E2%80%93-quick-start-guide/4399905).
- [Use automated Autopilot device preparation with Windows 365 Frontline Cloud PCs in shared mode (preview)](/windows-365/enterprise/autopilot-device-preparation).
- [What is Windows 365 Frontline?](/windows-365/enterprise/introduction-windows-365-frontline)
