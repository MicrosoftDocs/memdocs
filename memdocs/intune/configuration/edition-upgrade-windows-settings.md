---
# required metadata

title: Windows 10 upgrade and S mode settings in Microsoft Intune - Azure | Microsoft Docs
description: See a list of all the settings, and what they do when upgrading a Windows 10 edition on a device, or enable S mode on a device using a device configuration profile in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/29/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Windows 10 (and newer) device settings to upgrade editions or enable S mode in Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

Microsoft Intune includes many settings to help manage and protect your devices. This article describes some of the settings to upgrade editions or enable S mode on Windows 10 devices. These settings are created in an upgrade configuration profile in Intune that are pushed or deployed to devices.

As part of your mobile device management (MDM) solution, use these settings to control the edition and S mode options for your Windows 10 devices.

For more information on this feature, see [Upgrade Windows 10 editions or enable S mode](edition-upgrade-configure-windows-10.md).

## Before you begin

Create a [Windows 10 edition upgrade and mode switch device configuration profile](edition-upgrade-configure-windows-10.md#create-the-profile).

## Edition upgrade

- **Edition to upgrade to**: Select the Windows 10 edition that you're upgrading to. The devices targeted by this policy are upgraded to the edition you choose.
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
