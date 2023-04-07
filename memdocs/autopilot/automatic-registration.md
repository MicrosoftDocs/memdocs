---
title: Automatic registration of existing devices
description: Automatically add devices to Windows Autopilot.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/10/2023
ms.topic: how-to
ms.collection: 
  - M365-modern-desktop
  - m365initiative-coredeploy
  - tier2
---

# Automatic registration of existing devices

*Applies to:*

- Windows 11
- Windows 10
- Windows Holographic, version 2004

## Requirements

You can automatically register an existing device if it's:

- Running a [supported version](/windows/release-information/) of Windows
- Enrolled in an MDM service such as Intune
- A corporate device that's not already registered with Autopilot

For devices that meet these requirements, the MDM service can ask the device for the hardware hash. After it has that, it can automatically register the device with Windows Autopilot.

For more information on how to do this with Microsoft Intune, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile) and review the description of the **Convert all targeted devices to Autopilot** setting. See the following example:

![Convert all targeted devices.](images/convert-devices.png)

> [!NOTE]
> Using the setting **Converting all targeted devices to Autopilot** in the Autopilot profile doesn't automatically convert existing hybrid Azure AD device in the assigned group(s) into an Azure AD device. The setting only registers the devices in the assigned group(s) for the Autopilot service. For more information, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile).

## Windows Autopilot for existing devices

When using the [Windows Autopilot for existing devices](existing-devices.md) scenario, you don't need to pre-register the devices with Windows Autopilot. Instead, a configuration file (AutopilotConfigurationFile.json) containing all the Windows Autopilot profile settings is used. The device can then be registered with Windows Autopilot using the same **Convert all targeted devices to Autopilot** setting.

## Also see

[Registration overview](registration-overview.md)
