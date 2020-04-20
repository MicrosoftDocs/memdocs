---
title: Scenarios to deploy enterprise operating systems
titleSuffix: Configuration Manager
description: Learn about several scenarios to deploy enterprise operating systems with Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Scenarios to deploy enterprise operating systems with Configuration Manager

*Applies to: Configuration Manager (current branch)*

The following OS deployment scenarios are available in Configuration Manager:  

#### Upgrade Windows to the latest version
This scenario upgrades the OS on computers that currently run Windows 7, Windows 8.1, or Windows 10. The upgrade process keeps the applications, settings, and user data on the computer. There are no external dependencies, such as the Windows ADK. This process can be faster and more resilient than traditional OS deployments.  

For more information, see [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md).


#### Windows Autopilot for existing devices
<!--3607717, fka 1358333-->
Starting in version 1810, Windows Autopilot for existing devices is available with Windows 10 version 1809 or later. This feature allows you to reimage and provision a Windows 7 device for Windows Autopilot user-driven mode using a single Configuration Manager task sequence.

For more information, see [Windows Autopilot for existing devices](windows-autopilot-for-existing-devices.md).


#### Refresh an existing computer with a new version of Windows
This scenario partitions and formats (wipes) an existing computer and installs a new OS on the computer. You can migrate settings and user data after the OS is installed.  

For more information, see [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### Install a new version of Windows on a new computer (bare metal)
This scenario installs an OS on a new computer. It's a fresh installation of the OS and doesn't include any settings or user data migration.  

For more information, see [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md).


#### Replace an existing computer and transfer settings
This scenario installs an OS on a new computer. Optionally, you can migrate settings and user data from the old computer to the new computer.  

For more information, see [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md).


