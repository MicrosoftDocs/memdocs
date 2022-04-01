---
# required metadata
title: Microsoft Teams on Cloud PCs
titleSuffix:
description: Learn about using Microsoft Teams on a Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/23/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: spatnaik
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Microsoft Teams on a Cloud PC

Microsoft Teams is one of the core Microsoft 365 applications used with Windows 365. The [Windows 10/11 images optimized for Microsoft 365 apps](device-images.md#gallery-images) available in the Windows 365 image gallery support Teams chat, presence, calling, and meeting optimizations.

Using Microsoft Teams on a Cloud PC is different from using it on a physical PC. You will need to do the following to provide the best Teams experiences from Cloud PCs:

- Read the [requirements and limitations](/microsoftteams/teams-for-vdi) for using Microsoft Teams in virtualized environments.
- [Prepare your network](/microsoftteams/prepare-network/) for Microsoft Teams.
- Confirm that [required components](/azure/virtual-desktop/teams-on-avd) for Microsoft Teams optimizations are installed.
- Conform to [Cloud PCs sizing requirements](cloud-pc-size-recommendations.md) for Microsoft Teams.
- Conform to [End-user hardware requirements](end-user-hardware-requirements.md) for Microsoft Teams.

## Teams optimizations

The [Windows 10/11 images](device-images.md#gallery-images) in the gallery are pre-configured with required optimization components. When you install and use Microsoft Teams in your cloud PC you get an optimized experience. These optimization components enable peer-to-peer audio and video calls from your physical endpoint to the other person's endpoint. This creates the same experience as you would have on a physical endpoint running Microsoft Teams.

Some of the key benefits of the optimizations are:

- High-performance peer-to-peer streaming facilitated by WebRTC and rendered directly on the endpoint.
- Devices are redirected as the same hardware device, resulting in better hardware redirection support.
- Windows 10/11 and macOS endpoints get all the benefits of the modern media stack, including HW video decoding.

### Supported endpoints

Media optimization for Microsoft Teams is only available for the Windows and macOS endpoints. Media optimizations require:

- Remote Desktop client for Windows version 1.2.1026.0 or later (ideally the latest version).
- Remote Desktop client for macOS version 10.7.7 or later ([preview](..\public-preview.md)). If you upgrade from versions earlier than 10.7.7, you'll also need to go to Microsoft **Remote Desktop Preferences** > **General** and turn on Teams optimizations. If you're using the client for the first time and already have version 10.7.7 or later installed, you won't need to do this. In that case, Teams optimizations are turned on by default.

> [!NOTE]
> Microsoft Teams installs during the first sign in to the Cloud PC. Installation can take a couple of minutes. Make sure to restart Teams to activate the AV optimizations that redirect audio and video. You can also sign out and in again to your Cloud PC to gain the same result.

## Known issues and limitations

The following are known issues and limitations:

- Video calling
  - Only one video stream from an incoming camera or screen share stream is supported. When there's an incoming screen share, that screen share is shown, instead of the video of the dominant speaker.
  - Sharing outgoing camera and screen simultaneously isn’t supported. You can only share your desktop or webcam, not both at the same time.
  - Incoming and outgoing video stream resolution is limited to 720p resolution.

- Audio calling
  - Teams doesn't switch to use the last audio device that a user selected, if the device is disconnected, and then reconnected.
  - Shared system audio while presenting your desktop isn’t supported.

- Sharing
  - Give control and take control: Supported during a PowerPoint sharing session. Not supported during a screen sharing or application sharing session.

- General calling and meetings
  - Creation of Live events isn’t possible. You can attend Live events.

- macOS
  - Audio devices can't be configured from the Teams app, and the client automatically uses the default client audio device. To switch audio devices, configure settings from the client audio preferences instead.

The following calling and meeting features are not supported:

- Video calling
  - Video background effects (blur, image)
  - Video 3x3 gallery view
  - Dynamic video call quality

- Sharing
  - Sharing applications
  - Sharing local client desktop

- General calling and meetings
  - Live reactions (Like, Heart, Applause, Laugh and Surprised)
  - QOS setting for Teams
  - Support for http proxies
  - Enhanced emergency services (e911)
  - Call Me
  - Live captions
  - Transcription
  - Remote volume control support
  - Multi-window (MW) functionality

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

[Assign apps to a Cloud PC](assign-apps.md)
