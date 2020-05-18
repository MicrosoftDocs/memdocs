---
# required metadata
title: Upgrade to Windows Holographic for Business in Microsoft Intune - Azure | Microsoft Docs
description: Upgrade to Windows 10 Holographic for Business using a device configuration profile in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Upgrade devices running Windows Holographic to Windows Holographic for Business

Microsoft Intune includes many settings to help manage and protect your devices. This article lists and describes the settings to upgrade Windows Holographic devices to Windows Holographic for Business.

As part of your mobile device management (MDM) solution, use these settings to upgrade your Windows Holographic devices. For the Microsoft HoloLens, you can purchase the Commercial Suite to get the required license for the upgrade. For more information, see [Unlock Windows Holographic for Business features](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

As an Intune administrator, you can create and assign these settings to your devices.

For more information on this feature, see [Upgrade Windows 10 editions or enable S mode](edition-upgrade-configure-windows-10.md).

## Before you begin

[Create a Windows 10 edition upgrade and mode switch device configuration profile](edition-upgrade-configure-windows-10.md#create-the-profile).

When you create a Windows 10 edition upgrade and mode switch device configuration profile, there are more settings than what's listed in this article. The settings in this article are supported on Windows Holographic for Business devices.

## Edition upgrade

- **Edition to upgrade to**: Select **Windows 10 Holographic for Business**.
- **License File**: Browse to and select the XML license file that was provided to you.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="In Intune, enter the XML file name that includes the Holographic for Business license information.":::

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

You can also create edition upgrade profiles for [Windows 10 and later](edition-upgrade-windows-settings.md) devices.
