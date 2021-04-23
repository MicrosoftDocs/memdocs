---
title: Windows Autopilot software requirements
ms.reviewer: 
manager: laurawi
description: Inform yourself about software requirements for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, Autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: conceptual
ms.custom: 
- CI 116757
- CSSTroubleshooting
---


# Windows Autopilot software requirements

**Applies to**

- Windows 10
- Windows Holographic, version 2004 or later

Windows Autopilot depends on specific features available in Windows 10, Azure Active Directory, and MDM services, such as Microsoft Intune. To use Windows Autopilot and access these features, some software requirements must be met.

**Note**: For a list of OEMs that currently support Windows Autopilot, see the Participant device manufacturers section at [Windows Autopilot](https://aka.ms/windowsAutopilot).

## Software requirements

### HoloLens

- Windows Autopilot for HoloLens 2 requires Windows Holographic, version 2004 or later.  For more information, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

### Windows 10

- A [supported version](/windows/release-information/) of Windows 10 Semi-Annual Channel is required. Windows 10 Enterprise 2019 long-term servicing channel (LTSC) is also supported.
- The following editions are supported:
  - Windows 10 Pro
  - Windows 10 Pro Education
  - Windows 10 Pro for Workstations
  - Windows 10 Enterprise
  - Windows 10 Education
  - Windows 10 Enterprise 2019 LTSC

### Protocols

- Azure Active Directory (AAD) requires both WS-Trust and WS-Federation protocols.

>[!NOTE]
>Procedures for deploying Windows Autopilot might refer to specific products and versions. The inclusion of these products in this content doesn't imply an extension of support for a version that is beyond its support lifecycle. Windows Autopilot does not support products that are beyond their support lifecycle. For more information, see [Microsoft Lifecycle Policy](/lifecycle/).

## Next steps

[Windows Autopilot networking requirements](networking-requirements.md)
