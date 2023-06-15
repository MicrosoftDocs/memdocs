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
ms.service: windows-365
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
ms.collection:
- M365-identity-device-management
- tier2
---

# Applications in Windows 365

As an IT admin, one of the easiest ways to get started with Windows 365 is to create Cloud PCs with default gallery images of Windows 10/11 Enterprise. After provisioning, you can customize the user experience by using Microsoft Endpoint Manager to push apps to your users’ Cloud PCs. These images can include existing Windows client apps already in your Microsoft Endpoint Manager environment. Since these Cloud PC devices are enrolled in Endpoint Manager, you can treat them like any other Windows device in your environment.

The following apps are available with no need to upload:

- [Microsoft 365 Apps for Enterprise](/mem/intune/apps/apps-add-office365) (formerly Office 365 Pro Plus)
- Microsoft Teams
- Microsoft OneDrive
- [Microsoft Edge](/mem/intune/apps/apps-windows-edge)

## Supported application formats in Windows 365

### .IntuneWin  

The IntuneWin format is a way to pre-process Windows classic (Win32) apps. The tool converts application installation files into the intunewin format.  

After you use this tool on the app installer folder, you can create an app enrollment configuration for enhanced deployment capabilities. For example, OS version dependencies and uninstall methods when you need to remove applications remotely.  

If you select the most common application format (Win32), you must encapsulate the .exe or .msi file into a IntuneWin file. Windows 365 needs this encapsulation as part of the App configuration set.  

### .MSI  

MSI format installers are supported by both the Line of Business and Windows app (win32) options within Intune. The latter is more enhanced for app dependencies.  

### MSIX  

MSIX is Microsoft’s new Windows app package format that provides a modern packaging experience to all Windows apps. The MSIX package format preserves the functionality of existing app packages and install files. It also enables new, modern packaging and deployment features to Win32, WPF, and Windows Forms apps.  

MSIX combines the best features of MSI, .appx, App-V.

### AppX  

Also known as modern (UWP) apps. Files with an AppX extension added are ready for distribution and installation.  

Within the Windows Store as part of Windows 10/11 Enterprise, apps are automatically distributed as AppX – UWP format.  

AppX is helpful for distributing applications supported for multiple devices, including PCs, tablets, and smartphones that run on Windows.

## Office

Windows 365 Cloud PCs only support the Microsoft 365 Apps version of Office. For more information about the differences between Microsoft 365 Apps and other versions of Office, see [About Microsoft 365 Apps in the enterprise](/deployoffice/about-microsoft-365-apps).

## Universal Print

[Universal Print](/universal-print/fundamentals/universal-print-whatis) is a modern print solution that organizations can use to simplify their print infrastructure through cloud services from Microsoft. You can use Universal Print with Windows 365 Enterprise, either natively or through one of the Universal Print [partners](/universal-print/fundamentals/universal-print-partner-integrations). Legacy print-server environments are also possible to use together with Windows 365.

For information on Universal Print requirements, see [Universal Print printer provisioning tool](/universal-print/fundamentals/universal-print-intune-tool).

For information on setting up Universal Print with a Windows 365 Enterprise hybrid Azure Active Directory configuration, see [Enable Hybrid AD/AAD Environment on Universal Print](/universal-print/fundamentals/universal-print-hybrid-ad-aad-environment-setup).

<!-- ########################## -->
## Next steps

[Assign apps to a Cloud PC](assign-apps.md)
