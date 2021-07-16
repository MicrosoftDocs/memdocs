---
# required metadata
title: Accessing Cloud PCs - Azure | Microsoft Docs
titleSuffix:
description: Learn how end users can access their Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 06/03/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: alcort
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Access a Cloud PC

End users can access their Cloud PCs in two different ways:

- [www.microsoft.com/windows-365?rtc=1](https://www.microsoft.com/windows-365?rtc=1)
- Microsoft Remote Desktop

## Windows365 web site

End users can navigate to [www.microsoft.com/windows-365?rtc=1](https://www.microsoft.com/windows-365?rtc=1) to access their Cloud PCs.  

(Screenshot of end user portal.)

### Requirements

To access their Cloud PC from this website, the end user's device must meet the following requirements:

- Supported OS versions: Windows, macOS, ChromeOS, Linux
- A modern browser like Microsoft Edge, Google Chrome, Safari, or Mozilla Firefox (v55.0 and later).

### End-user actions

While on soft.com, end users can perform actions on their Cloud PCs by selecting the gear icon on a Cloud PC card.

(Screenshot of card with gear icon selected.)

- **Rename**: Changes the name of the Cloud PC shown to the user on web site. This action won’t affect any name in MEM, AAD, on the device, or in the Remote Desktop Apps.  
- **Restart**: Restarts the Cloud PC.
- **Troubleshoot**: Troubleshoot and attempt to resolve any issues that may be preventing a user from connecting to their Cloud PC. The checks run include checking whether any files or agents required for connectivity are correctly installed and ensuring that the Azure resources are available.

  | Return state | Description |
  | ------------- | ------------- |
  | No issues detected | None of the checks ran discovered an issue with the Cloud PC. |
  | Issues resolved  | An issue was detected and fixed. |
  | Can’t connect to Cloud PC. We’re working to fix it, try again later. | A Microsoft service required for connectivity is unavailable. Try connecting again later. |
  | We couldn’t fix issues with your Cloud PC. Contact your administrator. | An issue was detected but it was unable to be fixed. This could be due to a ongoing Windows update or another issue. If this error persists for an extended period of time the Cloud PC may need to be reprovisioned. |

## Remote Desktop

The Microsoft Remote Desktop app lets users access and control a remote PC, including a Cloud PC.

For a list of clients by operating system, see [Remote Desktop clients](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients).

### Install the Microsoft Remote Desktop app

To set up their Remote Desktop client, users follow these steps:

1. Download the Remote Desktop app from the Download App page on [www.microsoft.com/windows-365?rtc=1](https://www.microsoft.com/windows-365?rtc=1).
2. Select **Subscribe**.
3. Enter their Azure Active Directory credentials.
4. The Cloud PC appears in the list, and they can double-click it to launch.

### End user hardware requirements for accessing Cloud PCs

Hardware requirements vary depending on which Microsoft Remote Desktop client the end user installs.

#### Microsoft Remote Desktop client for Windows

Downloads available for:

- [Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2068602)
- [Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2098960)

Requirements:

- **Operating systems**: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2
- **CPU**: 1vCPU with 1 GHz or faster processor
- **RAM**: 1024 MB
- **Hard drive**: 100 MB or more
- **.NET Framework version**: 4.6.1 or later
- **Video**: DirectX 9 or later with WDDM 1.0 driver

If you'll be using Microsoft Teams on the Cloud PCs, the following Window device requirements increase to:

- **CPU**: At least 2vCPU with Minimum 1.6 GHz or faster processor. For higher video/screen share resolution and frame rate, a 4-core processor or better is recommended.
- **RAM**: 1024 MB
- **Hard drive**: 3 GB or more
- **.NET Framework version**: 4.6.1 or later
- **Video**: DirectX 9 or later with WDDM 1.0 driver. Background video effects require Windows 10 or a processor with AVX2 instruction set. Also, Teams audio and video offloading on a Cloud PC benefits from a dedicated Graphics Processing Unit (GPU) within the device.

#### Microsoft Remote Desktop client for Windows from the Microsoft Store

Download from the [Microsoft Store](https://www.microsoft.com/store/p/microsoft-remote-desktop/9wzdncrfj3ps).

Requirements:

- **Operating systems**: Windows 10 1703 or later
- **CPU**: 1 GHz or faster processor
- **RAM**: 1024 MB
- **Hard drive**: 100 MB or more
- **Video**: DirectX 9 or later with WDDM 1.0 driver. Teams audio and video offloading on Cloud PC benefits from a dedicated Graphics Processing Unit (GPU) within your physical endpoint device.

#### macOS, iOS/iPadOS, and Android

You can install the client and find requirements for other platforms here:

- [macOS](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12)
- [iOS/iPadOS](https://aka.ms/rdios)
- [Android](https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx)

<!-- ########################## -->
## Next steps

For information about the different protocol network requirements per scenario, see [Network requirements](requirements-network.md).
