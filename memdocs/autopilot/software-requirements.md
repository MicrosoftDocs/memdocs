---
title: Windows Autopilot software requirements
description: Inform yourself about software requirements for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, Autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 11/12/2021
ms.collection:
  - M365-modern-desktop
  - highpri
ms.topic: conceptual
ms.custom: 
- CI 116757
- CSSTroubleshooting
---


# Windows Autopilot software requirements

**Applies to**

- Windows 11
- Windows 10
- Windows Holographic, version 2004 or later

Windows Autopilot depends on specific features available in Windows client, Azure Active Directory (Azure AD), and MDM services, such as Microsoft Intune. To use Windows Autopilot and access these features, some software requirements must be met.

> [!NOTE]
> For a list of OEMs that currently support Windows Autopilot, see the Participant device manufacturers section at [Windows Autopilot](https://aka.ms/windowsAutopilot).

## Software requirements

### Windows 11

Use a supported version of Windows 11. For more information, see [Windows release health](/windows/release-health/).

The following editions are supported: Pro, Pro Education, Pro for Workstations, Enterprise, and Education

### HoloLens

- Windows Autopilot for HoloLens 2 requires Windows Holographic, version 2004 or later.  For more information, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

### Windows 10

- A [supported version](/windows/release-health/) of Windows 10 Semi-Annual Channel or Windows 10 General Availability Channel is required. 
- The following editions are supported:
  - Windows 10 Pro
  - Windows 10 Pro Education
  - Windows 10 Pro for Workstations
  - Windows 10 Enterprise
  - Windows 10 Education

> [!NOTE]
> Procedures for deploying Windows Autopilot might refer to specific products and versions. The inclusion of these products in this content doesn't imply an extension of support for a version that is beyond its support lifecycle. Windows Autopilot does not support products that are beyond their support lifecycle. For more information, see [Microsoft Lifecycle Policy](/lifecycle/).

## Next steps

[Windows Autopilot networking requirements](networking-requirements.md)
