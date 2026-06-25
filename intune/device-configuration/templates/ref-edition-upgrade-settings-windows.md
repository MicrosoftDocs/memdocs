---
title: Windows upgrade and S mode settings in Microsoft Intune
description: See a list of all the settings, and what they do when upgrading a Windows edition on a device, or switch out of S mode on a device using a device configuration profile in Microsoft Intune.
ms.date: 06/23/2026
ms.topic: reference
ms.reviewer: mikedano
ms.collection:
- M365-identity-device-management
---

# Windows device settings to upgrade editions or enable S mode in Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

Microsoft Intune includes many settings to help manage and protect your devices. This article describes some of the settings to upgrade Windows client editions, or switch out of S mode on Windows devices. Create these settings in an upgrade configuration profile in Intune and assign or deploy the profile to devices.

As part of your mobile device management (MDM) solution, use these settings to control the Windows client edition and Windows 10 S mode options for your Windows devices.

For more information on this feature, see [Upgrade Windows editions or enable S mode](./configure-edition-upgrade-windows.md).

For information on other options to upgrade Windows editions, see [Windows edition upgrade](/windows/deployment/upgrade/windows-10-edition-upgrades).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> This feature supports the following platform:
> - Windows
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To configure this policy and start collecting inventory data from devices, use an account with at least one of the following roles:
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../../includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> - Create a [Windows edition upgrade and mode switch device configuration profile](./configure-edition-upgrade-windows.md#create-the-profile).
:::column-end:::
:::row-end:::

## Edition upgrade

- **Edition to upgrade to**: Select the Windows edition that you want to upgrade to. The devices targeted by this policy upgrade to the edition you choose. When set to **Not configuration**, Intune doesn't change or update this setting.
- **Product Key**: Enter the product key that you received from Microsoft. After you create the policy with the product key, you can't update the key. For security reasons, the key is hidden. To change the product key, enter the entire key again.
- **License File**: For **Windows Holographic for Business**, browse and select the license file you received from Microsoft. This license file includes license information for the editions you're upgrading the devices to.

## Mode switch

- **Switch out of S mode**: Switches the device out of S mode. Your options:

  - **No configuration**: Intune doesn't change or update this setting. By default, the S mode device might stay in S mode. User can switch the device out of S mode.
  - **Keep in S mode**: Prevents users from switching the device out of S mode.
  - **Switch**: Allows users to switch the device out of S mode.

## Related articles

- [Assign the profile](../assign-device-profile.md), and [monitor its status](../monitor-device-profile.md).
- Create edition upgrade profiles for [Windows Holographic for Business](./ref-holographic-upgrade-settings.md) devices.
