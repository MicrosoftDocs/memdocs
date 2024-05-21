---
title: Overview of Windows Autopilot device preparation
description: Windows Autopilot device preparation is used to set up and configure new devices, getting them ready for productive use.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/27/2024
ms.topic: article
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
  - essentials-overview
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
- Near real-time detailed deployment reporting.

> [!NOTE]
>
> This article is for **Windows Autopilot device preparation**. For **Windows Autopilot**, see [Overview of Windows Autopilot](../windows-autopilot.md).

## Requirements

- Windows 11, version 23H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later.
- Windows 11, version 22H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later.

- Microsoft Entra ID - Only Microsoft Entra join is supported.

- Device shouldn't be registered or added as a Windows Autopilot device - If the device is registered or added as Windows Autopilot device, the Windows Autopilot profile takes precedence over the Windows Autopilot device preparation policy. If a device needs to be removed as a Windows Autopilot device, see [Deregister a device](../registration-overview.md#deregister-a-device).

For additional detailed requirements, see [Windows Autopilot device preparation requirements](requirements.md).

## Process overview

When new Windows devices are initially deployed, Windows Autopilot device preparation uses the OEM-optimized version of Windows client. The OEM-optimized version of Windows client is preinstalled on the device, so custom images and drivers don't need to be maintained for every device model. Instead of re-imaging the device, with Windows Autopilot device preparation, the existing Windows installation can be transformed into a "business-ready" state that can:

- Deliver Windows Autopilot device preparation configuration during user authentication in the out-of-box experience (OOBE).
- Automatically add devices to the security group and receive selected applications and Powershell scripts assigned to the group.

## Windows Autopilot device preparation improvements

Windows Autopilot device preparation is an improved profile experience that incorporates common customer asks. It improves the onboarding experience by providing a profile experience to deploy configurations efficiently, consistently, and remove the complexity out of troubleshooting. Its goal is to be:

- Simple.
- Fast.
- Observable.
- Reliable.

New features in Windows Autopilot device preparation include:

- **Utilizing enrollment time grouping in Intune** - Device is added to a security group at enrollment time and configuration is delivered immediately. This feature provides a faster and more reliable setup.  For more information, see [Enrollment Time Grouping](#enrollment-time-grouping).
- **Out of the box granular reporting** - Out of the box reporting and monitoring with near real-time status of deployments, including applications and PowerShell scripts details and deployment time. This feature provides improved troubleshooting. For more information, see [Windows Autopilot device preparation reporting and monitoring](reporting-monitoring.md).
- **Support for Government Community Cloud High (GCCH) and Department of Defense (DoD) environments** - Windows Autopilot device preparation supports [GCCH and DoD](/mem/intune/fundamentals/intune-govt-service-description) environments.

## Key features and capabilities

The key features of Windows Autopilot device preparation include:

- Enrollment time grouping.
- Faster and more reliable setup.
- Granular reporting.
- Improved troubleshooting.

Windows Autopilot device preparation capabilities include:

- User-driven deployment flow.
- Standard user access requirement.
- Application and PowerShell script selection during OOBE.
- Simplified and clear OOBE user experience.
- Detailed deployment report for better admin troubleshooting.

## Improved experiences

## Admin experience

Windows Autopilot device preparation simplifies admin configuration by having a single profile to provision all policies in one location, including deployment and OOBE settings.

### User experience

Windows Autopilot device preparation also improves the user experience in the following ways:

- A simplified view during OOBE where the percentage of progress is displayed.
- The experience is more consistent.
- The user is informed when the OOBE setup is complete.
- When issues arise, logs can be exported with ease.
- The end-user gets to the desktop faster.

## Troubleshooting and Reporting

Windows Autopilot device preparation offers near real-time status updates on deployments. Windows Autopilot device preparation reporting includes detailed application and PowerShell script information and deployment time, allowing for improved troubleshooting and reporting.

Deployment report captures status of each deployment:

- Easily track which devices went through Autopilot.
- Track status and deployment phase in near real-time.
- More details for each deployment:
  - Device details.
  - Profile name and version.
  - Deployment status details.
  - Apps applied with status.
  - Scripts applied with status.

## Enrollment Time Grouping

The key to Windows Autopilot device preparation is Enrollment Time Grouping. It consists of the following phases:

- **Configure applications and policies to a security group** - User authenticates and the Windows Autopilot device preparation configuration is delivered.
- **Select applications and PowerShell scripts to get installed during OOBE** - Selected applications and PowerShell scripts assigned to the group are installed. The device joins the security group.
- **Intune pre-calculates applications and policies** - User gets to the desktop. Remaining configuration is applied.

## Corporate identifiers for Windows

Windows Autopilot device preparation supports the Intune corporate identifier enrollment feature. Corporate identifiers in Intune allows pre-uploading of Windows device identifiers (serial number, manufacturer, model) and ensures only trusted devices go through Windows Autopilot device preparation. This feature is optional for Windows Autopilot device preparation and isn't required for a Windows Autopilot device preparation deployment to work. For more information, see:

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
