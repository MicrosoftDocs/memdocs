---
title: Overview of Windows Autopilot device preparation
description: Windows Autopilot Preparation is used to set up and pre-configure new devices, getting them ready for productive use.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/08/2024
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

Windows Autopilot device preparation is used to set up and pre-configure new devices, getting them ready for productive use. Windows Autopilot device preparation aims to simplify device deployment by delivering consistent configurations, enhancing the overall setup speed, and improving troubleshooting capabilities.

This article explores the capabilities of the Windows Autopilot device preparation, its benefits for administrators, and the user experience it offers including:

- Reducing the time IT spends on deploying devices.
- Reducing the infrastructure required to maintain the devices.
- Maximizing ease of use for all types of end users.

> [!NOTE]
>
> This article is for **Windows Autopilot device preparation**. For **Windows Autopilot**, see [Overview of Windows Autopilot][../windows-autopilot.md]

## Requirements

- Windows 11 23H2 with April CU or newer
- Microsoft Entra ID join.

## Process overview

When new Windows devices are initially deployed, Windows Autopilot Preparation uses the OEM-optimized version of Windows client. The OEM-optimized version of Windows client is preinstalled on the device, so custom images and drivers don't need to be maintained for every device model. Instead of re-imaging the device, with Windows Autopilot device preparation, the existing Windows installation can be transformed into a "business-ready" state that can:

- Configure apps and policies for a security group.
- Select apps and scripts to be installed during OOBE (Out-of-Box Experience).
- Assign the Windows Autopilot device preparation profile to users.
- Deliver Windows Autopilot device preparation configuration during user authentication in OOBE.
- Automatically add devices to the security group and receive selected apps and scripts assigned to the group.

## Windows Autopilot device preparation improvements

Windows Autopilot device preparation is an improved profile experience which incorporates common customer asks and improves the onboarding experience by providing a profile experience to deploy configurations efficiently, consistently, and remove the complexity out of troubleshooting. It's goal is to be:

- Simple.
- Fast.
- Observable.
- Reliable.

With theses goals, Windows Autopilot device preparation should provide:

- Simplicity.
- Consistency and reliability.
- Improved insights.
- Improved user friendliness.

Features new in Windows Autopilot device preparation include:

- **Enrollment time grouping** - Device is added to a security group at enrollment time and configuration is delivered immediately. This provides a faster and more reliable setup.
- **Granular reporting** - Near real-time status of deployments, including applications and scripts details and deployment time. This provides improved troubleshooting.

## Key features and capabilities

The key features of Windows Autopilot Preparation include:

- Enrollment time grouping.
- Faster and more reliable setup.
- Granular reporting.
- Improved troubleshooting.

Windows Autopilot device preparation capabilities include:

- User-driven deployment flow.
- Standard user access requirement.
- Application and script selection during OOBE.
- Simplified and clear OOBE user experience.
- Detailed deployment report for better admin troubleshooting.

## User experience

One of the improvements of Windows Autopilot device preparation is the user experience:

- A simplified view during OOBE where the percentage of progress is displayed.
- The experience is more consistent.
- The user is informed when the OOBE setup is complete.
- When issues arise, logs can be exported with ease.

## Troubleshooting and Reporting

Windows Autopilot device preparation offers near real-time status updates on your deployments, including detailed application and script information and deployment time, allowing for improved troubleshooting and reporting.

- Deployment report captures status of each deployment:

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

- **Configure apps and policies to a security group** - User authenticates and the Windows Autopilot device preparation configuration is delivered.
- **Select apps and scripts to get installed during OOBE** - Selected apps and scripts assigned to the group are installed. The device joins the security group.
- **Intune pre-calculates apps and policies** - User gets to the desktop. Remaining configuration is applied.

## Tutorial

For tutorials with detailed instructions on configuring Windows Autopilot device preparation, see the [Windows Autopilot device preparation tutorials](/tutorial/autopilot-device-preparation-scenarios.md).

## Related content

- [Windows Autopilot device preparation FAQs](faq.yaml).
- [Windows Autopilot device preparation tutorial](tutorial/scenarios.md).
- [Windows Autopilot device preparation requirements](requirements.md).
- [Windows Autopilot device preparation reporting and monitoring](reporting-monitoring.md).
- [Windows Autopilot device preparation known issues](known-issues.md).
