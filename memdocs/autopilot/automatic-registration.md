---
title: Automatic registration of existing devices - Windows Autopilot
description: Automatically add devices to Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 11/05/2021
ms.topic: how-to
ms.collection: 
- M365-modern-desktop
- m365initiative-coredeploy
---

# Automatic registration of existing devices

**Applies to**

- Windows 11
- Windows 10
- Windows Holographic, version 2004

## Requirements

You can automatically register an existing device if it's:

- Running a [supported version](/windows/release-information/) of Windows
- Enrolled in an MDM service such as Intune
- A corporate device that's not already registered with Autopilot

> [!NOTE]
> Converting all targeted devices to Autopilot isn't supported for transforming a hybrid Azure AD device into a Azure AD Autopilot device.<!-- MEMDocs#2175 -->

For devices that meet these requirements, the MDM service can ask the device for the hardware hash. After it has that, it can automatically register the device with Windows Autopilot.

For more information on how to do this with Microsoft Intune, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile) and review the description of the **Convert all targeted devices to Autopilot** setting. See the following example:

![Convert all targeted devices.](images/convert-devices.png)

## Windows Autopilot for existing devices

When using the [Windows Autopilot for existing devices](existing-devices.md) scenario, you don't need to pre-register the devices with Windows Autopilot. Instead, a configuration file (AutopilotConfigurationFile.json) containing all the Windows Autopilot profile settings is used. The device can then be registered with Windows Autopilot using the same **Convert all targeted devices to Autopilot** setting.

## Also see

[Registration overview](registration-overview.md)
