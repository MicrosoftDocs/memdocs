---
title: Automatic registration of existing devices
description: Automatically add devices to Windows Autopilot.
ms.service: windows-client
ms.subservice: itpro-autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.topic: how-to
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - tier2
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Automatic registration of existing devices

## Requirements

An existing device can automatically register if it's:

- Running a [supported version](/windows/release-information/) of Windows
- Enrolled in a mobile device management (MDM) service such as Intune
- A corporate device that isn't already registered with Autopilot

For devices that meet these requirements, the MDM service can ask the device for the hardware hash. After it has that, it can automatically register the device with Windows Autopilot.

For more information on how to automatically register devices for Windows Autopilot with Microsoft Intune, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile) and review the description of the **Convert all targeted devices to Autopilot** setting. See the following example:

:::image type="content" source="images/convert-devices.png" alt-text="Screenshot that shows how to convert all targeted devices.":::

> [!NOTE]
>
> Using the setting **Convert all targeted devices to Autopilot** in the Autopilot profile doesn't automatically convert existing hybrid Microsoft Entra device in the assigned groups into a Microsoft Entra device. The setting only registers the devices in the assigned groups for the Autopilot service. For more information, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile).

## Windows Autopilot for existing devices

When the [Windows Autopilot for existing devices](existing-devices.md) scenario is used, devices don't need to be preregistered with Windows Autopilot. Instead, a configuration file (AutopilotConfigurationFile.json) containing all the Windows Autopilot profile settings is used. The device can then be registered with Windows Autopilot using the same **Convert all targeted devices to Autopilot** setting.

## Related content

- [Registration overview](registration-overview.md).
