---
title: Overview of Windows Autopilot Device Preparation
description: Windows Autopilot Preparation is used to set up and pre-configure new devices, getting them ready for productive use.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/26/2024
ms.topic: article
ms.custom: QuickDraft
search.appverid: MET150
ai-usage:
- ai-assisted
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
  - essentials-overview
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Overview of Windows Autopilot Device Preparation

Windows Autopilot Device Preparation is used to set up and pre-configure new devices, getting them ready for productive use. Windows Autopilot Device Preparation aims to simplify device deployment by delivering consistent configurations, enhancing the overall setup speed, and improving troubleshooting capabilities.

This article explores the capabilities of the Windows Autopilot Device Preparation, its benefits for administrators, and the user experience it offers including:

- Reducing the time IT spends on deploying devices.
- Reducing the infrastructure required to maintain the devices.
- Maximizing ease of use for all types of end users.

> [!NOTE]
>
> This article is for Windows Autopilot Device Preparation. For the original Windows Autopilot, see [Overview of Windows Autopilot][../windows-autopilot.md]

## Requirements

- Windows 11 23H2 with April CU or newer

## Process overview

When new Windows devices are initially deployed, Windows Autopilot Preparation uses the OEM-optimized version of Windows client. The OEM-optimized version of Windows client is preinstalled on the device, so custom images and drivers don't need to be maintained for every device model. Instead of re-imaging the device, with Windows Autopilot Device Preparation, the existing Windows installation can be transformed into a "business-ready" state that can:

- Configure apps and policies for a security group.
- Select apps and scripts to be installed during OOBE (Out-of-Box Experience).
- Assign the Windows Autopilot Device Preparation profile to users.
- Deliver Windows Autopilot Device Preparation configuration during user authentication in OOBE.
- Automatically add devices to the security group and receive selected apps and scripts assigned to the group.

After signing in, users are presented with a new status page in the Company Portal that:

- Displays compliance status and allows users to remediate.
- Shows the status of remaining required apps.
- Provides a clear indication that device setup is complete.

## Windows Autopilot Device Preparation improvements

Windows Autopilot Device Preparation aims to improve over the original [Windows Autopilot][../windows-autopilot.md] by providing a profile experience to deploy configurations efficiently, consistently, and remove the complexity out of troubleshooting. It's goal is to be:

- Simple
- Fast
- Observable
- Reliable

by providing the following features:

- Simplicity.
- Consistency and reliability.
- Insights.
- User friendliness.

New features in Windows Autopilot Device Preparation include:

- Enrollment time grouping - Device is added to a security group at enrollment time and configuration is delivered immediately. This provides a faster and more reliable setup.
- Granular reporting - Near real-time status of deployments, including applications and scripts details and deployment time. This provides improved troubleshooting.

## Key features and capabilities

The key features of Windows Autopilot Preparation include:

- Enrollment time grouping.
- Faster and more reliable setup.
- Granular reporting.
- Improved troubleshooting.

Windows Autopilot Device Preparation capabilities include:

- User-driven deployment flow.
- Standard user access requirement.
- Application and script selection during OOBE.
- Simplified and clear OOBE user experience.
- Detailed deployment report for better admin troubleshooting.

## User experience

One of the improvements of Windows Autopilot Device Preparation is the user experience:

- A simplified view during OOBE where the percentage of progress is displayed.
- The experience is more consistent.
- The user is informed when the OOBE setup is complete.
- When issues arise, logs can be exported with ease.

In addition to the streamlined experience during OOBE, the experience is also improved at first sign-on and in the Company Portal:

- After the user signs on for the first time:

  - The Company Portal is automatically launched after the user signs in for the first time to display the status page.
  - The user can access the Desktop while additional configurations and applications are applied.

- In the Company Portal, the user can:

  - See compliance and if necessary, remediate.
  - See status for remaining required applications.
  - See clear indication that device setup is complete.

### Troubleshooting and Reporting

Windows Autopilot Device Preparation offers near real-time status updates on your deployments, including detailed application and script information and deployment time, allowing for improved troubleshooting and reporting.

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

The key to Windows Autopilot Device Preparation is Enrollment Time Grouping. It consists of the following phases:

- **Configure apps and policies to a security group** - User authenticates and the Windows Autopilot Device Preparation configuration is delivered.
- **Select apps and scripts to get installed during OOBE** - Selected apps and scripts assigned to the group are installed. The device joins the security group.
- **Intune pre-calculates apps and policies** - User gets to the desktop. Remaining configuration is applied.

## Tutorial

For tutorials with detailed instructions on configuring Windows Autopilot Device Preparation, see the [Windows Autopilot Device Preparation tutorials](/tutorial/autopilot-device-preparation-scenarios.md).

## Related content
