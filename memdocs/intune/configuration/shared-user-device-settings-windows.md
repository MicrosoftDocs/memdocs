---
# required metadata

title: Windows 10/11 shared device settings - Microsoft Intune
description: Add and use Windows 10/11 to configure devices that are shared, or used by multiple users in Microsoft Intune. See a list of all the settings and what they do on the devices, including Microsoft Surface. Control guest accounts, manage accounts and delete inactive accounts, allow or prevent saving to local storage, set power and sleep options, choose when updates are installed, and use devices in education environments in a device configuration profile.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/20/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection:
- tier3
- M365-identity-device-management
---

# Windows 10/11 and newer settings to manage shared devices using Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

Windows 10/11 client devices, such as the Microsoft Surface, can be used by many users. Devices that have multiple users are called shared devices, and are a part of mobile device management (MDM) solutions.

Using Microsoft Intune, end-users can sign in to these shared devices with a guest account. As they use the device, they only get access to features you allow. As the Intune administrator, you configure access, choose when accounts are deleted, control power management settings, and more for your shared Windows client devices.

This article describes some of the settings you can configure in a device configuration profile. When the profile is created in Intune, you deploy or assign the profile to device groups in your organization. You can also assign this profile to device groups with mixed device types and Windows OS versions.

For more information on this feature in Intune, see [Control access, accounts, and power features on shared PC or multi-user devices](shared-user-device-settings.md). For more information on the Windows CSP, see [SharedPC CSP](/windows/client-management/mdm/sharedpc-csp).

## Before your begin

Create a [Windows 10/11 shared multi-user device configuration profile](shared-user-device-settings.md).

## Shared multi-user device settings

These settings use the [SharedPC CSP](/windows/client-management/mdm/sharedpc-csp).

- **Shared PC mode**: **Enable** turns on shared PC mode. In this mode, only one user signs in to the device at a time. Another user can't sign in until the first user signs out. When set to **Not configured** (default), Intune doesn't change or update this setting.
- **Guest account**: Choose to create a Guest option on the sign-in screen. Guest accounts don't require any user credentials or authentication. This setting creates a new local account each time it's used. Your options:
  - **Guest**: Only allows a local guest account to sign in to the device.
  - **Domain**: Only allows an Azure Active Directory (AD) domain account to sign in to the device.
  - **Guest and domain**: Allows a local guest account, or an Azure Active Directory (AD) domain account to sign in to the device.
- **Account management**: Choose if accounts are automatically deleted. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Enabled**: Accounts created by guests, and accounts in AD and Azure AD are automatically deleted from the devices. When a user signs off the device, or when system maintenance runs, these accounts are removed from the devices.

    Also enter:

    - **Account Deletion**: Choose when accounts are deleted:
      - **At storage space threshold**
      - **At storage space threshold and inactive threshold**
      - **Immediately after log-out**

    Also enter:

    - **Start delete threshold(%)**: Enter a percentage (0-100) of disk space. When the total disk/storage space drops below the value you enter, the cached accounts are deleted. It continuously deletes accounts to reclaim disk space. Accounts that are inactive the longest are deleted first.
    - **Stop delete threshold(%)**: Enter a percentage (0-100) of disk space. When the total disk/storage space meets the value you enter, the deleting stops.
    - **Inactive account threshold**: Enter the number of consecutive days before deleting the account that hasn't signed in, from 0-60 days.

  - **Disabled**: The local, AD, and Azure AD accounts created by guests stay on the device, and aren't deleted.

- **Local Storage**: With local storage, users can save and view files on the device's hard drive. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Enabled**: Allows users to see and save files locally using File Explorer.
  - **Disabled**: Prevents users from saving and viewing files on the device's hard drive.

- **Power Policies**: Allow or prevent users from changing the power settings. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Enabled**: Users can hibernate the device, can close the lid to sleep the device, and change the power settings.
  - **Disabled**: Users can't turn off hibernate, can't override all sleep actions (such as closing the lid), and can't change the power settings.

- **Sleep time out (in seconds)**: Enter the number of inactive seconds (0-18000) before the device goes into sleep mode. `0` means the device never sleeps. If you don't set a time, the device goes to sleep after 3600 seconds (60 minutes).

- **Sign-in when PC wakes**: Choose if users must sign in after the device comes out of sleep mode. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Enabled**: Requires users to sign in with a password when device comes out of sleep mode.
  - **Disabled**: Users don't have to enter their username and password.

- **Maintenance start time (in minutes from midnight)**: Enter the time in minutes (0-1440) when automatic maintenance tasks, such as Windows Update, run. The default start time is midnight, or zero (`0`) minutes. Change the start time by entering a start time in minutes from midnight. For example, if you want maintenance to begin at 2 AM, enter `120`. If you want maintenance to begin at 8 PM, enter `1200`.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

- **Education policies**: Choose if policies for education environment are enabled. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Enabled**: Uses the recommended settings for devices used in schools, which are more restrictive.
  - **Disabled**: The default and recommended education policies aren't used.

  For more information on what the education policies do, see [Windows 10 configuration recommendations for education customers](/education/windows/configure-windows-for-education).

> [!TIP]
> [Set up a shared or guest PC](/windows/configuration/set-up-shared-or-guest-pc) (opens another docs web site) is a great resource on this Windows client feature, including concepts and group policies that can be set in shared mode.

## Next steps

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- See the settings for [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
