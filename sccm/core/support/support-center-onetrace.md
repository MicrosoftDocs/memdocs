---
title: Support Center OneTrace (Preview)
titleSuffix: Configuration Manager
description: OneTrace is a new log viewer with Support Center that has improvements over CMTrace.
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Support Center OneTrace (Preview)

<!--3555962-->

Starting in version 1906, OneTrace is a new log viewer with Support Center. It works similarly to CMTrace, with the following improvements:

- A tabbed view
- Dockable windows
- Improved search capabilities
- Ability to enable filters without leaving the log view
- Scrollbar hints to quickly identify clusters of errors
- Fast log opening for large files

![Screenshot of OneTrace log viewer](media/3555962-onetrace.png)

OneTrace works with many types of log files, such as:

- Configuration Manager client logs
- Configuration Manager server logs
- Status messages
- Windows Update ETW log file on Windows 10
- Windows Update log file on Windows 7 & Windows 8.1

## Prerequisites

- .NET Framework version 4.6 or later

## Install

OneTrace installs with Support Center. Find the Support Center installer on the site server at the following path: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

> [!Note]  
> Support Center and OneTrace use Windows Presentation Foundation (WPF). This component isn't available in Windows PE. Continue to use CMTrace in boot images with task sequence deployments.  

## See also

- [Support Center log viewer](/sccm/core/support/support-center-ui-reference#bkmk_log-viewer)

- [CMTrace](/sccm/core/support/cmtrace)
