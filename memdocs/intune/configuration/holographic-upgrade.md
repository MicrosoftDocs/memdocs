---
# required metadata
title: Upgrade to Windows Holographic for Business
titleSuffix: Microsoft Intune
description: Learn how to ugrade devices running Windows Holographic to Window Holographic for Business
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
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

Microsoft Intune includes many settings to help manage and protect your devices. This article lists and describes the settings to upgrade Windows Holographic devices to Windows Holographic for Business. These settings are created in an upgrade configuration profile in Intune that are pushed or deployed to devices.

As part of your mobile device management (MDM) solution, use these settings to upgrade your Windows Holographic devices. For the Microsoft HoloLens, you can purchase the Commercial Suite to get the required license for the upgrade. For more information, see [Unlock Windows Holographic for Business features](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

For more information on this feature, see [Upgrade Windows 10 editions or enable S mode](../edition-upgrade-configure-windows-10.md).

## Before you begin

[Create a device configuration profile](edition-upgrade-configure-windows-10.md#create-the-profile).

## Edition upgrade

- **Edition to upgrade to**: Select **Windows 10 Holographic for Business**.
- **License File**: Browse to and select the XML license file that was provided to you.

  ![Enter the XML file name that includes the Holographic for Business license information](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## Next steps

The profile is created, but it may not be doing anything yet. Be sure to [assign the profile](device-profile-assign.md), and [monitor its status](../device-profile-monitor.md).

You can also create edition upgrade profiles for [Windows 10 and later](edition-upgrade-windows-settings.md) devices.
