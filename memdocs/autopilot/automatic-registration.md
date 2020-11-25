---
title: Automatic registration of existing devices
ms.reviewer: 
manager: laurawi
description: How to add devices to Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.topic: how-to
ms.collection: 
- M365-modern-desktop
- m365initiative-coredeploy
---

# Automatic registration of existing devices

**Applies to**

- Windows 10
- Windows Holographic, version 2004

You can automatically register an existing device if it's:
- running a supported version of Windows 10 semi-annual channel.
- enrolled in an MDM service such an Intune.

For devices that meet both these requirements, the MDM service can ask the device for the hardware hash. After it has that, it can automatically register the device with Windows Autopilot.

For instructions on how to do this with Microsoft Intune, see [Create an Autopilot deployment profile](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) documentation describing the "Convert all targeted devices to Autopilot" setting. 

You can automatically convert such devices to Windows using Intune's **Convert all targeted devices to Autopilot** setting. For more information, see [Create an Autopilot deployment profile](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile). 

When using the [Windows Autopilot for existing devices](existing-devices.md) scenario, you don't need to pre-register the devices with Windows Autopilot. Instead, a configuration file (AutopilotConfigurationFile.json) containing all the Windows Autopilot profile settings is used. The device can then be registered with Windows Autopilot using the same "Convert all targeted devices to Autopilot" setting.

