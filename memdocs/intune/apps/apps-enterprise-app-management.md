---
title: Enterprise App Management in Microsoft Intune
titleSuffix:
description: Learn about Enterprise App Management and the Enterprise App Catalog in Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/08/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 
ms.reviewer: dguilory
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Enterprise App Management in Microsoft Intune

Enterprise App Management (EAM) enables you to easily discover prepackaged Enterprise App Catalog apps (Win32) contained in the Enterprise App catalog in Microsoft Intune. The Enterprise App Catalog is a collection of Win32 apps that have been designed and prepared by Microsoft to support Intune. The catalog contains both Microsoft apps and third-party apps. 

An Enterprise App Catalog app (Win32) in Microsoft Intune is a Windows app that you can be added via the Enterprise App Catalog. This app type leverages the Win32 platform and has support for customizable capabilities. The Enterprise App Catalog is a collection of prepackaged [Win32 apps](../apps/apps-win32-app-management.md) that have been designed and prepared by Microsoft to support Intune. The catalog contains both Microsoft apps and third-party apps. 

> [!IMPORTANT]
> Enterprise App Management is an Intune add-on as part of the Intune suite that is available for trial and purchase. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Enterprise App Management (EAM) encompasses the aspects of working with Win32 apps from the Enterprise App Catalog. The catalog offers a variety of Win32 apps that have been wrapped using the [Intune App Wrapping Tool](../developer/apps-prepare-mobile-application-management.md#intune-app-wrapping-tool). In addition, these apps have been [prepared as Win32 apps](../apps/apps-win32-prepare.md).

## Benefits of EAM

The benefits of using Enterprise App Management are the following:

- **Streamlined app management**: You can save time and reduce complexity by streamlining the app management process. Discover and package apps directly from the Intune console.
- **Reduce security risks and vulnerabilities**: Mitigate risk and deploy app fixes immediately when security vulnerabilities are discovered.
- **Stay current with updates**: You will be able to keep apps up-to-date and secure by identifying and updating outdated applications using guided updating and update signal.

When adding an Enterprise App Catalog app, you can specify the following installation details:

- Commands to install and uninstall the app
- Time required to install the app
- Option to allow the app to be uninstalled
- Installation and device restart behavior
- Return codes to indicate post-installation behavior

You can specify the following requirements that devices must meet before the app is installed:

- Windows OS architecture required
- Minimum OS required
- Disk spaced required
- Physical memory required
- Minimum number of processors required
- Minimum CPU speed required
- Additional File, Registry, and Script requirement rules

You can also configure app specific rules used to detect the presence of the Enterprise App Catalog app where you can choose to either manually configure the detection rules or use a custom script to detect the presence of the app before installing the app.

## Self updating apps

EAM offers support for self updating app capabilities. You can select a minimum target version. Intune will ensure the app is at least at the target minimum version, but will consider the app installed if the version of the app is above the minimum version. Your EAM app will auto-update based on the app venders process, keeping your app up-to-date as quickly as possible. Also, you will be able to see the installed version on the device.

## Next steps

- [Add an Enterprise App Catalog app (Win32) to Microsoft Intune](../apps/apps-add-enterprise-app.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
