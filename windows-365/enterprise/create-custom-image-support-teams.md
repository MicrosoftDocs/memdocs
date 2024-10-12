---
# required metadata
title: Create a custom Cloud PC image to support Microsoft Teams
titleSuffix:
description: Learn how to create a custom Cloud PC image to support Microsoft Teams.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/28/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chbrinkh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Create a Cloud PC custom image that supports Microsoft Teams

During the initial setup of your tenant, we recommend that you provision your Cloud PCs with the Windows 10/11 Enterprise + Microsoft 365 images available in the image gallery. These images give you the benefit of having all the Office applications optimized and pre-installed without the need for any extra level of configuration.

If you want to create custom images that don’t include the optimizations for Microsoft Teams, you'll need you perform the following steps in your custom image. These steps make sure your image has the correct registry settings and policies to support Teams.

The following steps are only needed when you aren’t using the Windows 365 gallery images with Microsoft 365 pre-installed. You can also use the gallery image to create your custom image. If you do so, you also don’t have to perform the steps below.

1. Create the following registry setting key required custom images in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Teams:
    - Name: IsWVDEnvironment
    - Type: DWORD
    - Value: 1
2. Install the [latest Visual C++ runtime](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads). This runtime is required for the Teams WebRTC protocol redirection to work.
3. Install the [WebRTC Redirector (websocket) plugin](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RWNg9F). For instructions on how to install, see [Install the Teams WebSocket Service](/azure/virtual-desktop/teams-on-avd#install-the-teams-websocket-service). The plugin is required for Teams to function properly in a Cloud PC environment with the optimizations.

> [!NOTE]
> Don’t install the Microsoft Teams desktop application. If you want Microsoft Teams on the Cloud PC, install Microsoft 365 Apps + Teams by using Microsoft Intune.

## Verify that Teams optimizations loaded successfully

If you need to verify that Teams optimizations are working on a Cloud PC (for an end user, for example), tell the Cloud PC user to follow these steps:

1. In Microsoft Teams, select the ellipses (**…**) in the menu bar > **About** > **Version**.
2. Confirm that **WVD Media Optimized** is listed alongside the version. If it is, you’re ready to test the better experience.

If media optimizations loaded successfully, the audio devices and cameras available locally are listed in the device menu. If the menu shows **Remote audio**, follow these steps:

1. Quit the Teams app and try again.
2. If the devices still don't appear in the menu, check the **Privacy settings** on your local PC. Make sure that **Allow apps to access your microphone** (under **Settings** > **Privacy** > **App permissions – Microphone**) is **On**.
3. Disconnect from the remote session.
4. Reconnect and check the audio and video devices again.

To join calls and meetings with video, you must also grant permission for apps to access your camera.

<!-- ########################## -->
## Next steps

[Assign apps to a Cloud PC](assign-apps.md)
