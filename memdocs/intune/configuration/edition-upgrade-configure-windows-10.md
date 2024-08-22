---
# required metadata

title: Upgrade Windows 10/11 edition or switch S mode using Intune policy
description: Use Microsoft Intune to upgrade Windows 10/11 client devices to a different edition, or switch S mode. Administrators can use a device configuration profile to upgrade Windows client Professional to Windows client Enterprise, and switch out of S mode. See the supported upgrade paths for Windows 10/11 Pro, N Edition, Education, Cloud, Enterprise, Core, and Holographic. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.assetid: ae8b6528-7979-47d8-abe0-58cea1905270

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Upgrade Windows 10/11 editions or switch out of S mode on devices using Microsoft Intune

You can create a Microsoft Intune policy that upgrades Windows editions, or switches out of S mode.

As part of your mobile device management (MDM) solution, you can upgrade your Windows 10/11 devices. For example, you want to upgrade your Windows 10 Professional devices to Windows 10 Enterprise. Or, you want the Windows 10 device to switch out of S mode.

[Windows 10 S mode](https://support.microsoft.com/help/4456067/windows-10-switch-out-of-s-mode) (opens another Microsoft web site) is designed for security and performance. You can use Intune to switch out of S mode. Switching out of S mode is one way. So once you switch out of S mode, you can't go back to Windows 10 S mode.

For more information, go to [commonly asked questions about S mode](https://support.microsoft.com/help/4020089/windows-10-in-s-mode-faq).

This feature applies to:

- Windows 11
- Windows 10
- Windows 10 1809 and newer for S mode
- Windows Holographic for Business

Intune uses **configuration profiles** to create and customize these settings for your organization's needs. After you add these features in a profile, you can then push or deploy the profile to Windows client devices in your organization. When you deploy the profile, Intune automatically upgrades the devices or switches out of S mode. When the device checks-in with the Intune service, the policy applies and Intune upgrades the device or switches out of S mode.

This article lists the supported upgrade paths, and shows you how to create the device configuration profile. For a list of all the available upgrade and S mode settings you can configure, go to [Windows client device settings to upgrade editions or enable S mode in Intune](edition-upgrade-windows-settings.md).

> [!NOTE]
> If you remove the policy assignment later, the version of Windows on the device isn't reverted. The device continues to run normally.

## Prerequisites

- To install the updated Windows version on the devices that you target with the policy (for Windows client Desktop editions), you need a valid product key. You can use either Multiple Activation Keys (MAK) or Key Management Server (KMS) keys.
- For Windows 10 Holographic editions, you can use a Microsoft license file. The license file includes the licensing information to install the updated edition on all devices that you target with the policy.
- The Windows client devices you assign the policy are enrolled in Microsoft Intune.
- To create the policy, at a minimum, sign in with an account that has the **Policy and Profile Manager** Intune role. For more information, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Supported upgrade paths

The following table lists the supported upgrade paths for the Windows 10 edition upgrade profile.

| Upgrade from | Upgrade to |
|---|---|
| Windows 10/11 Pro | Windows 10/11 Education <br/>Windows 10/11 Enterprise <br/>Windows 10/11 Pro Education |
| Windows 10/11 Pro N edition | Windows 10/11 Education N edition <br/>Windows 10/11 Enterprise N edition <br/>Windows 10/11 Pro Education N edition | 
| Windows 10/11 Pro Education | Windows 10/11 Education | 
| Windows 10/11 Pro Education N edition | Windows 10/11 Education N edition |
| Windows 10/11 Cloud | Windows 10/11 Education <br/>Windows 10/11 Enterprise <br/>Windows 10/11 Pro <br/>Windows 10/11 Pro Education | 
| Windows 10/11 Cloud N edition | Windows 10/11 Education N edition <br/>Windows 10/11 Enterprise N edition <br/>Windows 10/11 Pro N edition <br/>Windows 10/11 Pro Education N edition | 
| Windows 10/11 Enterprise | Windows 10/11 Education | 
| Windows 10/11 Enterprise N edition | Windows 10/11 Education N edition | 
| Windows 10/11 Core | Windows 10/11 Education <br/>Windows 10/11 Enterprise <br/>Windows 10/11 Pro Education | 
| Windows 10/11 Core N edition | Windows 10/11 Education N edition <br/>Windows 10/11 Enterprise N edition <br/>Windows 10/11 Pro Education N edition | 
| Windows 10 Holographic | Windows 10 Holographic for Business |

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Templates** > **Edition upgrade and mode switch**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile. For example, enter something like `Windows 10/11 edition upgrade profile` or `Windows 10 turn off S mode`.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, enter the settings you want to configure. For a list of all settings, and what they do, go to:

    - [Windows 10 upgrade and S mode](edition-upgrade-windows-settings.md)
    - [Windows Holographic for Business](holographic-upgrade.md)

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in with Intune, the policy applies.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

- See the upgrade and S mode settings for [Windows 10/11](edition-upgrade-windows-settings.md) and [Windows Holographic for Business](holographic-upgrade.md) devices.
