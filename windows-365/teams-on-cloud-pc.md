---
# required metadata
title: Microsoft Teams on Cloud PCs
titleSuffix:
description: Learn about using Microsoft Teams on a Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chbrinkh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Microsoft Teams on a Cloud PC

Microsoft Teams is one of the core Microsoft 365 applications used with Windows 365. The Microsoft 365 optimized Windows 10 image available in the Windows 365 image gallery supports Teams chat, presence, calling, and meeting optimizations.

Using Teams on a Cloud PC is different from using Teams on a physical PC environment. For more information about the limitations of Teams in virtualized environments, see [Teams for Virtualized Desktop Infrastructure](/microsoftteams/teams-for-vdi#known-issues-and-limitations).

> [!NOTE]
> Microsoft Teams installs during the first sign in to the Cloud PC. Installation can take a couple of minutes. Make sure to restart Teams to activate the AV optimizations that redirect audio and video. You can also sign out and in again to your Cloud PC to gain the same result.


## Teams optimizations

The image gallery provides Windows 10 Enterprise images pre-configured with all the software that’s needed for an optimized Teams experience on Cloud PCs. As an IT admin or user, you need only install and configure the Microsoft Teams application and then you are ready to use it.

The main benefit of this approach is that you setup the Teams audio and video call directly peer-to-peer from your physical endpoint to the other person. This creates the same experience as you would have on a physical endpoint running Microsoft Teams.

Some of the key benefits of the optimizations are:

- High-performance peer-to-peer streaming facilitated by WebRTC.Traffic flows peer-to-peer and is rendered by the endpoint.
- Devices are redirected as the same hardware device, resulting in better hardware redirection support.
- Windows 10 clients get all the benefits of the modern media stack, including HW video decoding.

### Teams optimization support

In Windows 365, optimization for Microsoft Teams is only available for:

- Windows Remote Desktop client on Windows 10 physical endpoints.
- Microsoft Teams client version 1.2.1026.0 and later.

## Known Teams issues and limitations

The following known issues are currently active when using Microsoft Teams as part of Windows 365:

- Teams on a Cloud PC only supports one incoming video input at a time. This means that whenever someone tries to share their screen, their screen will appear instead of the meeting leader's screen.
- Give control and take control aren't currently supported.
- Teams layout (like buttons) aren’t the same as on physical Teams.
- Reactions: Like, Heart Applause, and Laugh Emoticons in meetings aren’t supported.
- Creation of Live events isn’t possible. You can attend Live events.
- Save Audio and Camera device selection: when using multiple webcams you might have to re-select your primary webcam after signing back in.
- Sharing outgoing camera and screen simultaneously isn’t supported. You can only share your desktop or webcam, not both at the same time.
- Shared system audio while presenting your desktop isn’t supported.

The following features might experience issues when using Microsoft Teams as part of Windows 365:

- Background blur and effects  
- Remote Volume control support
- Video Call Quality
- Sharing the local client desktop from the remote app
- QOS setting for Teams
- Multi-window (MW) functionality
- Support for http proxies
- Enhanced emergency services (e911)
- MacOS & Linux Support
- Application sharing
- Call Me
- 1080p quality support
- Live Captions
- Give control and take control
- Transcripts
- Addition Video modes during a video call (3x3)
- Addition Video modes during a video call (7X7, together mode)

## Collect Teams logs for Microsoft support

If you encounter issues with the Teams desktop app in your Azure Virtual Desktop environment, collect client logs under %appdata%\Microsoft\Teams\logs.txt on the Cloud PC.

If you encounter issues with calls and meetings, collect Teams Web client logs with the key combination Ctrl + Alt + Shift + 1. Logs will be written to %userprofile%\Downloads\MSTeams Diagnostics Log DATE_TIME.txt on the Cloud PC.

### Contact Microsoft Teams support

For information on contacting Microsoft Teams support, see [Microsoft 365 admin center](/microsoft-365/admin/contact-support-for-business-products).

<!-- ########################## -->
## Next steps

[Assign apps to a Cloud PC](assign-apps.md)
