---
title: Scenarios to deploy enterprise operating systems
titleSuffix: Configuration Manager
description: Learn about several scenarios to deploy enterprise operating systems with Configuration Manager.
ms.date: 10/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Scenarios to deploy enterprise operating systems with Configuration Manager

*Applies to: Configuration Manager (current branch)*

The following OS deployment scenarios are available in Configuration Manager:  

## Upgrade Windows to the latest version

This scenario upgrades the OS on computers that run an earlier version of Windows. The upgrade process keeps the applications, settings, and user data on the computer. There are no external dependencies, such as the Windows ADK. This process can be faster and more resilient than traditional OS deployments.  

This scenario applies to all [supported versions](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) of Windows client and Windows Server.

For more information, see [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md).

## Windows Autopilot for existing devices
<!--3607717, fka 1358333-->

Windows Autopilot for existing devices is available with Windows 10, version 1809 or later. This feature allows you to reimage and provision a device with an earlier version of Windows for Windows Autopilot user-driven mode using a single Configuration Manager task sequence.

This scenario applies to Windows 10 version 1809 and later

For more information, see [Windows Autopilot for existing devices](../../../autopilot/existing-devices.md).

## Refresh an existing computer with a new version

This scenario partitions and formats an existing computer and installs a new OS on the computer. It's also referred to as _wipe and load_. You can migrate settings and user data after the OS is installed.

This scenario applies to all [supported versions](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) of Windows client and Windows Server.

For more information, see [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).

## Install a new version of Windows on a new computer

This scenario installs an OS on a new computer. It's also referred to as _bare metal_. It's a fresh installation of the OS and doesn't include any settings or user data migration.

This scenario applies to all [supported versions](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) of Windows client and Windows Server.

For more information, see [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md).

## Replace an existing computer and transfer settings

This scenario installs an OS on a new computer, and migrates settings and user data from an old computer to the new computer.

This scenario applies to all [supported versions](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) of Windows client and Windows Server.

For more information, see [Replace an existing computer and transfer settings](replace-an-existing-computer-and-transfer-settings.md).
