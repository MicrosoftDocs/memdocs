---
# required metadata
title: Optimize Zoom on a Windows 365 Cloud PC
titleSuffix:
description: Learn how to optimize Zoom on a Windows Cloud PC.
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

ms.reviewer: chbrink
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Optimize Zoom on a Windows 365 Cloud PC

Zoom is a 3rd-party application that provides online meeting services including support for virtualized environments like Windows 365 Cloud PCs. The instructions in this article help you optimize traffic for Zoom meetings when using the Microsoft Remote Desktop client on a Windows PC to access a Cloud PC.

To optimize Zoom, you’ll need to install the Zoom VDI Client on the Cloud PC and the Zoom Azure Virtual Desktop plugin on the local Windows PC that the user will use to access the Cloud PC.

> [!NOTE]  
> If you run into issues with Zoom for VDI on your Cloud PC, contact Zoom support.

## Requirements

- **Windows Remote Desktop Client**\*
- **Windows App**
- **Operating system**: Windows

\* These don't support connections through a web browser.

## Install the Zoom VDI client on the Cloud PC

1. Have the user sign in to the Cloud PC as a local administrator and, in their browser, navigate to the [Zoom VDI downloads and backwards compatibility page](https://support.zoom.us/hc/en-us/articles/360041602711).
2. Locate and download the most recent VDI client version.
3. Run the MSI and follow the installation instructions.

Alternatively, the admin can deploy the Zoom VDI client. For more information about deploying apps, see the [Win32 App management guide](/mem/intune/apps/apps-win32-app-management).

## Install the plugin on the local Windows PC

1. Sign in to the Windows PC that will be used to access the Cloud PC.
2. In a browser, navigate to the VDI release version page matching the page you used to install the VDI client. For example, [VDI Release Version 5.16.6]( https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0068823).
3. In the **Compatible Plugins** table, find the VDI client that you installed, and select the appropriate entry for **Azure Virtual Desktop**. For example, **Windows x86 or x64 (Phone and Meetings): 5.8.4.21112**. Only Windows clients are supported for these optimizations.
4. Run the MSI and follow the installation instructions.

> [!NOTE]  
> Zoom recommends that you use the same version numbers for both the VDI client and the plugin. Zoom doesn’t support running a plugin version higher than the VDI client version.

For more information on these installation steps, see Zoom’s [Getting started with VDI article]( https://support.zoom.us/hc/en-us/articles/360031096531-Getting-Started-with-VDI).

## To use the optimized Zoom client

To benefit from these optimizations, users must sign in to their Cloud PC from a Windows PC. After doing so, the user can open Zoom from the Cloud PC.

## Next steps

For more information about deploying apps, see the [Win32 App management guide](/mem/intune/apps/apps-win32-app-management).
