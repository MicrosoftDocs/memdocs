---
# required metadata
title: Applications with Windows 365
titleSuffix:
description: Learn how to use apps with Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/12/2021
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

# Applications in Windows 365

As an IT admin, one of the easiest ways to get started with Windows 365 is to create Cloud PCs with default gallery images of Windows 10 Enterprise. After provisioning, you can customize the user experience  by using Microsoft Endpoint Manager to push apps to your users’ Cloud PCs. These can include existing Windows 10 apps already in your Microsoft Endpoint Manager environment. Since these Cloud PC devices are enrolled in Endpoint Manager, you can treat these like any other Windows device in your environment.

The following apps are available with no need to upload:

- [Microsoft 365 Apps for Enterprise](/mem/intune/apps/apps-add-office365) (formerly Office 365 Pro Plus)
- Microsoft Teams
- Microsoft OneDrive
- [Microsoft Edge](/mem/intune/apps/apps-windows-edge)

## Supported application formats in Windows 365

### .IntuneWin  

The IntuneWin format is a way to pre-process Windows classic (Win32) apps. The tool converts application installation files into the .intunewin format.  

After you use this tool on the app installer folder, you can create an app enrollment configuration for enhanced deployment capabilities. For example, OS version dependencies and uninstall methods when you need to remove applications remotely.  

If you select the most common application format (Win32), you must encapsulate the .exe or .msi file into a IntuneWin file. Windows 365 needs this as part of the App configuration set.  

### .MSI  

MSI format installers are supported by both the Line of Business and Windows app (win32) options within Intune. The latter is more enhanced for app dependencies.  

### MSIX  

MSIX is Microsoft’s new Windows app package format that provides a modern packaging experience to all Windows apps. The MSIX package format preserves the functionality of existing app packages and/or install files. It also enables new, modern packaging and deployment features to Win32, WPF, and Windows Forms apps.  

MSIX combines the best features of MSI, .appx, App-V.

### AppX  

Also known as modern (UWP) apps. Files with an AppX extension added are ready for distribution and installation.  

Within the Windows Store as part of Windows 10 Enterprise, apps are automatically distributed as AppX – UWP format.  

AppX is very beneficial for distributing applications supported for multiple devices, including PCs, tablets, and smartphones that run on Windows.

## Universal Print


<!-- ########################## -->
## Next steps

[Assign apps to a Cloud PC](assign-apps.md)
