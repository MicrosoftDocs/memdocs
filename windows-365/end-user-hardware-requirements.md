---
# required metadata
title: End-user hardware requirements in Windows 365
titleSuffix:
description: Learn about the hardware requirements for end-users to access their Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/28/2021
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

# End-user hardware requirements to access a Cloud PC

To access their Cloud PC, an end-user's hardware must meet certain requirements. These requirements vary depending on which Microsoft Remote Desktop client the end-user installs.

## Microsoft Remote Desktop client for Windows

Downloads available for:

- [Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2068602)
- [Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2098960)

Hardware requirements:

- **Operating systems**: Windows 10/11, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2
- **CPU**: 1vCPU with 1 GHz or faster processor
- **RAM**: 1024 MB
- **Hard drive**: 100 MB or more
- **.NET Framework version**: 4.6.1 or later
- **Video**: DirectX 9 or later with WDDM 1.0 driver

If you'll be using Microsoft Teams on the Cloud PCs, the Windows device requirements increase to:

- **CPU**: At least 2vCPU with Minimum 1.6 GHz or faster processor. For higher video/screen share resolution and frame rate, a four-core processor or better is recommended.
- **RAM**: 4096 MB
- **Hard drive**: 3 GB or more
- **.NET Framework version**: 4.6.1 or later
- **Video**: DirectX 9 or later with WDDM 1.0 driver. Background video effects require Windows 10/11 or a processor with AVX2 instruction set. Also, Teams audio and video offloading on a Cloud PC benefits from a dedicated Graphics Processing Unit (GPU) within the device.

## Microsoft Remote Desktop client for Windows from the Microsoft Store

Download from the [Microsoft Store](https://www.microsoft.com/store/p/microsoft-remote-desktop/9wzdncrfj3ps).

Hardware requirements:

- **Operating systems**: Windows 10 1703 or later
- **CPU**: 1 GHz or faster processor
- **RAM**: 1024 MB
- **Hard drive**: 100 MB or more
- **Video**: DirectX 9 or later with WDDM 1.0 driver. Teams audio and video offloading on Cloud PC benefits from a dedicated Graphics Processing Unit (GPU) within your physical endpoint device.

## macOS, iOS/iPadOS, and Android

You can install the client and find requirements for other platforms here:

- [macOS](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12)
- [iOS/iPadOS](https://aka.ms/rdios)
- [Android](https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx)

## Linux

You can access Windows 365 Cloud PCs from your Linux OS devices by using:

- The web client available at windows365.microsoft.com.
- Third-party clients to connect to Azure Virtual Desktop, including:
  - [Dell](https://www.delltechnologies.com/asset/en-us/products/thin-clients/technical-support/dell-thinos-9-for-microsoft-wvd.pdf)
  - [HP](https://h20195.www2.hp.com/v2/GetDocument.aspx?docname=c07051097)
  - [IGEL](https://www.igel.com/igel-solution-family/)

  Third-party Linux client solutions can't be managed by using Microsoft Endpoint Manager. The partner provides a separate management tool for Linux devices.

<!-- ########################## -->
## Next steps

For information about the different protocol network requirements per scenario, see [Network requirements](./enterprise/requirements-network.md).