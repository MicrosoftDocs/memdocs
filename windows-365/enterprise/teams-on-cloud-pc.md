---
# required metadata
title: Microsoft Teams on Cloud PCs
titleSuffix:
description: Learn about using Microsoft Teams on a Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/01/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: spatnaik
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Microsoft Teams on a Cloud PC

Microsoft Teams is one of the core Microsoft 365 applications used with Windows 365. The [Windows 10/11 images optimized for Microsoft 365 apps](device-images.md#gallery-images) available in the Windows 365 image gallery support Teams chat, presence, calling, and meeting optimizations. Gallery images use the new [Microsoft Teams](/microsoftteams/new-teams-desktop-admin).

Using Microsoft Teams on a Cloud PC is different from using it on a physical PC. You'll need to do the following to provide the best Teams experiences from Cloud PCs:

- Read the [requirements and limitations](/MicrosoftTeams/vdi-2) for using Microsoft Teams in virtualized environments.
- [Prepare your network](/microsoftteams/prepare-network/) for Microsoft Teams.
- Confirm that [required components](/azure/virtual-desktop/teams-on-avd) for Microsoft Teams optimizations are installed.
- Conform to [Cloud PCs sizing requirements](cloud-pc-size-recommendations.md) for Microsoft Teams.
- Conform to [End-user hardware requirements](..\end-user-hardware-requirements.md) for Microsoft Teams.

## Teams optimizations

The [Windows 10/11 images](device-images.md#gallery-images) in the gallery are pre-configured with required optimization components. When you install and use new Microsoft Teams in your cloud PC, you get an optimized experience. These optimization components enable peer-to-peer audio and video calls from your physical endpoint to the other person's endpoint. This situation creates the same experience as you would have on a physical endpoint running Microsoft Teams.

Some of the key benefits of the optimizations are:

- High-performance peer-to-peer streaming facilitated by WebRTC and rendered directly on the endpoint.
- Devices are redirected as the same hardware device, resulting in better hardware redirection support.
- Windows 10/11 and macOS endpoints get all the benefits of the modern media stack, including HW video decoding.
- Teams optimization VDI 2.0 is currently not supported for macOS.

### Supported endpoints

Media optimization for Microsoft Teams is only available for the Windows and macOS endpoints. Media optimizations require:

- [Windows App for Windows](/azure/virtual-desktop/teams-on-avd) via the Microsoft Store (ideally the latest version).
- Remote Desktop client for Windows, version 1.2.1026.0 or later (ideally the latest version).
- Remote Desktop client for macOS, version 10.7.7 or later ([beta client](https://aka.ms/rdmacbeta)). If you upgrade from versions earlier than 10.7.7, you'll also need to go to Microsoft **Remote Desktop Preferences** > **General** and turn on Teams optimizations. If you're using the client for the first time and already have version 10.7.7 or later installed, you won't need to turn that on. In that case, Teams optimizations are turned on by default.

> [!NOTE]
> Microsoft Teams installs during the first sign in to the Cloud PC. Installation can take a couple of minutes. Make sure to restart Teams to activate the AV optimizations that redirect audio and video. You can also sign out and in again to your Cloud PC to gain the same result.

## Collect Teams logs for Microsoft support

If you encounter issues with the Teams desktop app in your Windows 365 environment, collect client logs on the Cloud PC under

```
%appdata%\Microsoft\Teams\logs.txt
```

If you encounter issues with calls and meetings, collect Teams Web client logs with the key combination Ctrl + Alt + Shift + 1. Logs will be written on the Cloud PC to

```
%userprofile%\Downloads\MSTeams Diagnostics Log DATE_TIME.txt
```

### Contact Microsoft Teams support

For information on contacting Microsoft Teams support, see [Microsoft 365 admin center](/microsoft-365/admin/contact-support-for-business-products).

<!-- ########################## -->
## Next steps

[Assign apps to a Cloud PC](assign-apps.md).

Learn about known issues, limitations, and how to log issues at [Troubleshoot Teams on Azure Virtual Desktop](/azure/virtual-desktop/troubleshoot-teams).
