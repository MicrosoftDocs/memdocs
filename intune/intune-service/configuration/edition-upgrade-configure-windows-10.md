---
title: Upgrade Windows editions or switch S mode using Intune policy
description: Use Microsoft Intune to upgrade Windows 10/11 client devices to a different edition, or switch S mode. Administrators can use a device configuration profile to upgrade Windows client Professional to Windows client Enterprise, and switch out of S mode. See the supported upgrade paths for Windows 10/11 Pro, N Edition, Education, Cloud, Enterprise, Core, and Holographic.
author: MandiOhlinger
ms.author: mandia
ms.date: 04/22/2024
ms.topic: how-to
ms.reviewer: mikedano
ms.collection:
- M365-identity-device-management
---

# Upgrade Windows editions or switch out of S mode on devices using Microsoft Intune

You can create a Microsoft Intune policy that upgrades Windows editions, or switches out of S mode.

As part of your mobile device management (MDM) solution, you can upgrade your Windows devices. For example, you want to upgrade your Windows Professional devices to Windows Enterprise. Or, you want the Windows device to switch out of S mode.

[Windows S mode](https://support.microsoft.com/help/4456067/windows-10-switch-out-of-s-mode) (opens another Microsoft web site) is designed for security and performance. You can use Intune to switch out of S mode. Switching out of S mode is one way. So once you switch out of S mode, you can't go back to Windows S mode.

For more information, go to [commonly asked questions about S mode](https://support.microsoft.com/help/4020089/windows-10-in-s-mode-faq).

This feature applies to:

- Windows
- Windows Holographic for Business

Intune uses **configuration profiles** to create and customize these settings for your organization's needs. After you add these features in a profile, you can then push or deploy the profile to Windows client devices in your organization. When you deploy the profile, Intune automatically upgrades the devices or switches out of S mode. When the device checks-in with the Intune service, the policy applies and Intune upgrades the device or switches out of S mode.

This article lists the supported upgrade paths, and shows you how to create the device configuration profile. For a list of all the available upgrade and S mode settings you can configure, go to [Windows client device settings to upgrade editions or enable S mode in Intune](edition-upgrade-windows-settings.md).

> [!NOTE]
> If you remove the policy assignment later, the version of Windows on the device isn't reverted. The device continues to run normally.

## Prerequisites

- To install the updated Windows version on the devices that you target with the policy (for Windows client Desktop editions), you need a valid product key. You can use either Multiple Activation Keys (MAK) or Key Management Server (KMS) keys.
- For Windows Holographic editions, you can use a Microsoft license file. The license file includes the licensing information to install the updated edition on all devices that you target with the policy.
- The Windows client devices you assign the policy are enrolled in Microsoft Intune.
- To create the policy, at a minimum, sign in with an account that has the **Policy and Profile Manager** Intune role. For more information, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Supported upgrade paths

The following table lists the supported upgrade paths for the Windows edition upgrade profile.

| Upgrade from | Upgrade to |
|---|---|
| Windows Pro | Windows Education <br/>Windows Enterprise <br/>Windows Pro Education |
| Windows Pro N edition | Windows Education N edition <br/>Windows Enterprise N edition <br/>Windows Pro Education N edition |
| Windows Pro Education | Windows Education |
| Windows Pro Education N edition | Windows Education N edition |
| Windows Cloud | Windows Education <br/>Windows Enterprise <br/>Windows Pro <br/>Windows Pro Education |
| Windows Cloud N edition | Windows Education N edition <br/>Windows Enterprise N edition <br/>Windows Pro N edition <br/>Windows Pro Education N edition |
| Windows Enterprise | Windows Education |
| Windows Enterprise N edition | Windows Education N edition |
| Windows Core | Windows Education <br/>Windows Enterprise <br/>Windows Pro Education |
| Windows Core N edition | Windows Education N edition <br/>Windows Enterprise N edition <br/>Windows Pro Education N edition |

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Templates** > **Edition upgrade and mode switch**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile. For example, enter something like `Windows edition upgrade profile` or `Windows - turn off S mode`.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, enter the settings you want to configure. For a list of all settings, and what they do, go to:

    - [Windows upgrade and S mode](edition-upgrade-windows-settings.md)
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

- See the upgrade and S mode settings for [Windows](edition-upgrade-windows-settings.md) and [Windows Holographic for Business](holographic-upgrade.md) devices.
