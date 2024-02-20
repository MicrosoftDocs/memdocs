---
title: Windows Autopilot software requirements
description: Inform yourself about software requirements for Windows Autopilot deployment.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/30/2023
ms.collection: 
  - M365-modern-desktop
  - highpri
  - tier1
ms.topic: conceptual
ms.custom: 
  - CI 116757
  - CSSTroubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a> 
---


# Windows Autopilot software requirements

Windows Autopilot depends on specific features available in Windows client, Microsoft Entra ID, and MDM services, such as Microsoft Intune. To use Windows Autopilot and access these features, some software requirements must be met.

> [!NOTE]
>
> For a list of OEMs that currently support Windows Autopilot, see the Participant device manufacturers section at [Windows Autopilot](https://www.microsoft.com/microsoft-365/windows/windows-autopilot).

## Software requirements

### Windows 11

A [supported version](/windows/release-health/) of Windows 11 General Availability Channel is required.

The following editions are supported:

- Windows 11 Pro
- Windows 11 Pro Education
- Windows 11 Pro for Workstations
- Windows 11 Enterprise
- Windows 11 Education

### Windows 10

A [supported version](/windows/release-health/) of Windows 10 General Availability Channel is required.

The following editions are supported:

- Windows 10 Pro
- Windows 10 Pro Education
- Windows 10 Pro for Workstations
- Windows 10 Enterprise
- Windows 10 Education

Windows 10 LTSC/LTSB editions aren't supported.

### HoloLens

- Windows Autopilot for HoloLens 2 requires Windows Holographic, version 2004 or later.  For more information, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

> [!NOTE]
>
> Procedures for deploying Windows Autopilot might refer to specific products and versions. The inclusion of these products in this content doesn't imply an extension of support for a version that is beyond its support lifecycle. Windows Autopilot doesn't support products that are beyond their support lifecycle. For more information, see [Microsoft Lifecycle Policy](/lifecycle/).

## Next steps

[Windows Autopilot networking requirements](networking-requirements.md)
