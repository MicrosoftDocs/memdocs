---
# required metadata

title: Windows 10 shared device settings - Microsoft Intune - Azure | Microsoft Docs
description: Add and use Windows 10 to configure devices that are shared, or used by multiple users in Microsoft Intune. See a list of all the settings and what they do on the devices, including Microsoft Surface. Control guest accounts, manage accounts and delete inactive accounts, allow or prevent saving to local storage, set power and sleep options, choose when updates are installed, and use devices in education environments in a device configuration profile.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/05/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
---

# Windows 10 and later settings to manage shared devices using Intune

Windows 10 and later devices, such as the Microsoft Surface, can be used by many users. Devices that have multiple users are called shared devices, and are a part of mobile device management (MDM) solutions.

Using Microsoft Intune, end-users can sign in to these shared devices with a guest account. As they use the device, they only get access to features you allow. As the Intune administrator, you configure access, choose when accounts are deleted, control power management settings, and more for your shared Windows 10 devices.

This article lists and describes the settings you use in a Windows 10 (and later) device configuration profile. When the profile is created in Intune, you deploy or assign the profile to device groups in your organization. You can also assign this profile to device groups with mixed device types and OS versions.

For more information on this feature in Intune, see [Control access, accounts, and power features on shared PC or multi-user devices](shared-user-device-settings.md). For more information on the Windows CSP, see [SharedPC CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

## Before your begin

[Create the profile](shared-user-device-settings.md).

## Shared multi-user device settings

These settings use the [SharedPC CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

- **Shared PC mode**: Choose **Enable** to turn on shared PC mode. In this mode, only one user signs in to the device at a time. Another user can't sign in until the first user signs out. **Not configured** (default) leaves this setting unmanaged by Intune, and doesn't push any policy to control this setting on a device.
- **Guest account**: Choose to create a Guest option on the sign-in screen. Guest accounts don't require any user credentials or authentication. This setting creates a new local account each time it's used. Your options:
  - **Guest**: Creates a guest account locally on the device.
  - **Domain**: Creates a guest account in Azure Active Directory (AD).
  - **Guest and domain**: Creates a guest account locally on the device, and in Azure Active Directory (AD).
- **Account management**: Set to **Enable** to automatically delete local accounts created by guests, and accounts in AD and Azure AD. When a user signs off the device, or when system maintenance runs, these accounts are deleted. When enabled, also set:
  - **Account Deletion**: Choose when accounts are deleted: **At storage space threshold**, **At storage space threshold and inactive threshold**, or **Immediately after log-out**. Also enter:
    - **Start delete threshold(%)**: Enter a percentage (0-100) of disk space. When the total disk/storage space drops below the value you enter, the cached accounts are deleted. It continuously deletes accounts to reclaim disk space. Accounts that are inactive the longest are deleted first.
    - **Stop delete threshold(%)**: Enter a percentage (0-100) of disk space. When the total disk/storage space meets the value you enter, the deleting stops.

  Set to **Disable** to keep the local, AD, and Azure AD accounts created by guests.

- **Local Storage**: Choose **Enabled** to prevent users from saving and viewing files on the device's hard drive. Choose **Disabled** to allow users to see and save files locally using File Explorer. **Not configured** (default) leaves this setting unmanaged by Intune, and doesn't push any policy to control this setting on a device.
- **Power Policies**: When set to **Enabled**, users can't turn off hibernate, can't override all sleep actions (such as closing the lid), and can't change the power settings. When set to **Disabled**, users can hibernate the device, can close the lid to sleep the device, and change the power settings. **Not configured** (default) leaves this setting unmanaged by Intune, and doesn't push any policy to control this setting on a device.
- **Sleep time out (in seconds)**: Enter the number of inactive seconds (0-18000) before the device goes into sleep mode. `0` means the device never sleeps. If you don't set a time, the device goes to sleep after 3600 seconds (60 minutes).
- **Sign-in when PC wakes**: Set to **Enabled** to require users to sign in with a password when device comes out of sleep mode. Choose **Disabled** so users don't have to enter their username and password. **Not configured** (default) leaves this setting unmanaged by Intune, and doesn't push any policy to control this setting on a device.
- **Maintenance start time (in minutes from midnight)**: Enter the time in minutes (0-1440) when automatic maintenance tasks, such as Windows Update, run. The default start time is midnight, or zero (`0`) minutes. Change the start time by entering a start time in minutes from midnight. For example, if you want maintenance to begin at 2 AM, enter `120`. If you want maintenance to begin at 8 PM, enter `1200`.
- **Education policies**: Choose **Enabled** to use the recommended settings for devices used in schools, which are more restrictive. Choose **Disabled** so the default and recommended education policies aren't used. **Not configured** (default) leaves this setting unmanaged by Intune, and doesn't push any policy to control this setting on a device.

  For more information on what the education policies do, see [Windows 10 configuration recommendations for education customers](https://docs.microsoft.com/education/windows/configure-windows-for-education).

- **Fast first sign-in**: Choose **Enabled** so users have a quick first sign-in experience. When **enabled**, the device automatically connects new non-admin Azure AD accounts to the pre-configured candidate local accounts. Choose **Disabled** to prevent the quick first sign-in experience. **Not configured** (default) leaves this setting unmanaged by Intune, and doesn't push any policy to control this setting on a device.

  [Authentication/EnableFastFirstSignIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-enablefastfirstsignin)

> [!TIP]
> [Set up a shared or guest PC](https://docs.microsoft.com/windows/intune/configuration/set-up-shared-or-guest-pc) (opens another docs web site) is a great resource on this Windows 10 feature, including concepts and group policies that can be set in shared mode.

## Next steps

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- See the settings for [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
