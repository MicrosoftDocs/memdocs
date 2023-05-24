---
# required metadata

title: Windows 10 upgrade and S mode settings in Microsoft Intune
description: See a list of all the settings, and what they do when upgrading a Windows 10 edition on a device, or switch out of S mode on a device using a device configuration profile in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/19/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Windows 10/11 device settings to upgrade editions or enable S mode in Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

Microsoft Intune includes many settings to help manage and protect your devices. This article describes some of the settings to upgrade Windows client editions, or switch out of S mode on Windows 10 devices. These settings are created in an upgrade configuration profile in Intune that are pushed or deployed to devices.

As part of your mobile device management (MDM) solution, use these settings to control the Windows client edition and Window 10 S mode options for your Windows devices.

This feature applies to:

- Windows 10

For more information on this feature, see [Upgrade Windows 10/11 editions or enable S mode](edition-upgrade-configure-windows-10.md).

For information on other options to upgrade Windows editions, see [Windows 10/11 edition upgrade](/windows/deployment/upgrade/windows-10-edition-upgrades).

## Before you begin

Create a [Windows 10/11 edition upgrade and mode switch device configuration profile](edition-upgrade-configure-windows-10.md#create-the-profile).

## Edition upgrade

- **Edition to upgrade to**: Select the Windows edition that you're upgrading to. The devices targeted by this policy are upgraded to the edition you choose.
- **Product Key**: Enter the product key that you received from Microsoft. After you create the policy with the product key, the key can't be updated, and is hidden for security reasons. To change the product key, enter the entire key again.
- **License File**: For **Windows 10 Holographic for Business**, choose **Browse** to select the license file you received from Microsoft. This license file includes license information for the editions you're upgrading the devices to.

## Mode switch

- **Switch out of S mode**: Switches the device out of S mode. Your options:

  - **No configuration**: Intune doesn't change or update this setting. By default, the S mode device might stay in S mode. User can switch the device out of S mode.
  - **Keep in S mode**: Prevents users from switching the device out of S mode.
  - **Switch**: Allows users to switch the device out of S mode.

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

You can also create edition upgrade profiles for [Windows Holographic for Business](holographic-upgrade.md) devices.
