---
title: Overview of Windows Autopilot device preparation
description: Windows Autopilot device preparation is used to set up and configure new devices, getting them ready for productive use.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/04/2025
ms.topic: overview
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
  - essentials-overview # this is the only article in Autopilot with this value
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Overview of Windows Autopilot device preparation

Windows Autopilot device preparation is used to set up and configure new devices, getting them ready for productive use. Windows Autopilot device preparation aims to simplify device deployment by delivering consistent configurations, enhancing the overall setup speed, and improving troubleshooting capabilities.

This article explores the capabilities of the Windows Autopilot device preparation, its benefits for administrators, and the user experience it offers including:

- Reducing the time IT spends on deploying devices.
- Reducing the infrastructure required to maintain the devices.
- Maximizing ease of use for all types of end users.
- Improved troubleshooting.
- Near real-time deployment status and monitoring.

> [!NOTE]
>
> This article is for **Windows Autopilot device preparation**. For **Windows Autopilot**, see [Overview of Windows Autopilot](../overview.md).

## Requirements

- Windows 11, version 24H2 or later.
- Windows 11, version 23H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later.
- Windows 11, version 22H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later.

- Microsoft Entra ID - only Microsoft Entra join is supported.

- Device shouldn't be registered or added as a Windows Autopilot device - if the device is registered or added as Windows Autopilot device, the Windows Autopilot profile takes precedence over the Windows Autopilot device preparation policy. If a device needs to be removed as a Windows Autopilot device, see [Deregister a device](../registration-overview.md#deregister-a-device).

For additional detailed requirements, see [Windows Autopilot device preparation requirements](requirements.md).

## Process overview

When new Windows devices are initially deployed, Windows Autopilot device preparation uses the OEM-optimized version of Windows client. The OEM-optimized version of Windows client is preinstalled on the device, so custom images and drivers don't need to be maintained for every device model. Instead of re-imaging the device, with Windows Autopilot device preparation, the existing Windows installation can be transformed into a "business-ready" state that can:

- Deliver Windows Autopilot device preparation configuration during device provisioning.

- Automatically add devices to the device security group and receive selected applications and PowerShell scripts assigned to the group.

## Windows Autopilot device preparation improvements

Windows Autopilot device preparation is an improved profile experience that incorporates common customer asks. It improves the onboarding experience by providing a profile experience to deploy configurations efficiently, consistently, and remove the complexity out of troubleshooting. Its goal is to be:

- Simple.
- Fast.
- Observable.
- Reliable.

New features in Windows Autopilot device preparation include:

- **Utilizing enrollment time grouping in Intune** - Device is added to a device security group at enrollment time and configuration is delivered immediately. This feature provides a faster and more reliable setup. For more information, see [Enrollment Time Grouping](#enrollment-time-grouping).

- **Granular reporting** - Improved monitoring and troubleshooting. Monitoring and reporting with near real-time status of deployments, including:

  - Applications status
  - PowerShell scripts status
  - Deployment time.
  For more information, see [Windows Autopilot device preparation reporting and monitoring](reporting-monitoring.md).
  
- **Support for Government Community Cloud High (GCCH) and Department of Defense (DoD) environments** - Windows Autopilot device preparation supports [GCCH and DoD](/mem/intune/fundamentals/intune-govt-service-description) environments.

> [!NOTE]
> [Windows 365 Frontline in shared mode](/windows-365/enterprise/introduction-windows-365-frontline) is not supported for GCCH and DoD at this time.

## Capabilities

Windows Autopilot device preparation capabilities include:

- Set up user-driven or automatic deployment flow.
- By default, making sure users are standard non-administrator users.
- Select application and PowerShell script to be delivered during device setup.
- Simplified and clear OOBE user experience with percentage progress indicator for user-driven flows.
- Deployment report for better troubleshooting.

## Improved experiences

### Admin experience

- Windows Autopilot device preparation simplifies admin configuration by having a single profile to provision all policies in one location, including deployment and OOBE settings.
- Line-of-business (LOB) and Win32 applications can be deployed in the same deployment.

### User experience

Windows Autopilot device preparation also improves the user experience in the following ways:

- A simplified view during OOBE where the percentage of progress is displayed.
- The experience is more consistent.
- The user is informed when the OOBE setup is complete.
- When issues arise, logs can be exported with ease.
- The end-user gets to the desktop faster.

### Troubleshooting and Reporting

Windows Autopilot device preparation offers near real-time status updates on deployments. Windows Autopilot device preparation monitoring includes application and PowerShell script status information, allowing for improved troubleshooting and reporting. Deployment monitoring includes the following features:

- Easily track which devices went through Autopilot.
- Track status and deployment phase for each device in near real-time.
- Each device has the following details in the monitoring report:
  - Device details.
  - Profile name and version.
  - Deployment status details.
  - Apps applied with status.
  - Scripts applied with status.

### Enrollment Time Grouping

The key to Windows Autopilot device preparation is Enrollment Time Grouping. With Enrollment Time Grouping, when a user authenticates into a device, the device is added to a pre-defined device security group during enrollment. Applications, scripts, and policies assigned to the device group are then deployed to the device. Direct assignment of devices to the device group allows the applications, scripts, and policies assigned to the device group to deploy quicker and more efficiently versus when using a dynamic device group.

Enrollment time grouping consists of the following phases:

- **Configure applications and policies to a security group** - User authenticates and the Windows Autopilot device preparation configuration is delivered.
- **Select applications and PowerShell scripts to get installed during OOBE** - Selected applications and PowerShell scripts assigned to the device security group are installed. The device also joins the device security group.

For Windows Autopilot device preparation:

- The device group is selected in the Windows Autopilot device preparation profile.
- Only applications and PowerShell scripts selected in the Windows Autopilot device preparation profile are deployed during OOBE. Any additional applications or PowerShell scripts assigned to the device group will be deployed after the Windows Autopilot device preparation deployment is complete.
- For policies, Windows Autopilot device preparation syncs any policies assigned to the device group. However, Windows Autopilot device preparation doesn't track if the policies are applied during the deployment. The policies might be applied either during the deployment or after the deployment is complete.

For more information, see [Enrollment time grouping in Microsoft Intune](/mem/intune/enrollment/enrollment-time-grouping).

### Corporate identifiers for Windows

Windows Autopilot device preparation supports the Intune corporate identifier enrollment feature. Corporate identifiers in Intune allows pre-uploading of Windows device identifiers (serial number, manufacturer, model) and ensures only trusted devices go through Windows Autopilot device preparation.

Windows Autopilot device preparation only requires corporate identifiers for Windows if Intune enrollment restrictions are being used to block personal device enrollments. For more information, see:

- [Identify devices as corporate-owned](/mem/intune/enrollment/corporate-identifiers-add).
- [What are enrollment restrictions?](/mem/intune/enrollment/enrollment-restrictions-set).
- [Create device platform restrictions](/mem/intune/enrollment/create-device-platform-restrictions).

## Tutorial

For tutorials with detailed instructions on configuring Windows Autopilot device preparation, see [Windows Autopilot device preparation scenarios](tutorial/scenarios.md).

## Related content

- [Windows Autopilot device preparation FAQs](faq.yml).
- [Windows Autopilot device preparation tutorial](tutorial/scenarios.md).
- [Windows Autopilot device preparation requirements](requirements.md).
- [Windows Autopilot device preparation reporting and monitoring](reporting-monitoring.md).
- [Windows Autopilot device preparation known issues](known-issues.md).
- [Windows Autopilot device preparation: What's new](whats-new.md).
