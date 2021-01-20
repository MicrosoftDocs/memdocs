---
title: Automatic registration of existing devices - Windows Autopilot
ms.reviewer: 
manager: laurawi
description: Automatically add devices to Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 12/16/2020
ms.topic: how-to
ms.collection: 
- M365-modern-desktop
- m365initiative-coredeploy
---

# Automatic registration of existing devices

**Applies to**

- Windows 10
- Windows Holographic, version 2004

## Requirements

You can automatically register an existing device if it's:
- running a [supported version](/windows/release-information/) of Windows 10 semi-annual channel, and
- enrolled in an MDM service such an Intune
- a corporate device that is not already registered with Windows Autopilot

For devices that meet both these requirements, the MDM service can ask the device for the hardware hash. After it has that, it can automatically register the device with Windows Autopilot.

For more information on how to do this with Microsoft Intune, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile) and review the description of the **Convert all targeted devices to Autopilot** setting. See the following example:

![Convert all targeted devices](images/convert-devices.png)

## Windows Autopilot for existing devices

When using the [Windows Autopilot for existing devices](existing-devices.md) scenario, you don't need to pre-register the devices with Windows Autopilot. Instead, a configuration file (AutopilotConfigurationFile.json) containing all the Windows Autopilot profile settings is used. The device can then be registered with Windows Autopilot using the same **Convert all targeted devices to Autopilot** setting.

## Also see

[Registration overview](registration-overview.md)