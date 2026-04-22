---
title: "Device Action: Remove Passcode"
description: Microsoft Intune remove passcode action helps you unlock devices remotely when users forget their passcodes. Discover how to use this feature.
#customer intent: As a help desk operator, I want to remove a forgotten passcode from a managed iOS device so that the user can regain access without wiping the device.
ms.date: 04/21/2026
ms.topic: how-to
---

# Device action: remove passcode

By using the *remove passcode* action in Microsoft Intune, you can remotely remove a device passcode. This action helps users regain access to their devices without requiring a full device wipe. this action is especially useful when a user forgets their passcode or is locked out of their device.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
> > - iOS/iPadOS

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote Tasks/Reset Passcode**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::

## How to remove a passcode from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Remove passcode**.

## User experience

After the passcode is removed, if there's a passcode policy set, the device prompts the user to set a new passcode in Settings.

> [!IMPORTANT]
> If the **Remove passcode** action fails, Intune might have stored the wrong unlock token. You need to **Wipe** the device to regain access.

## Reference links

- Microsoft Graph API: [resetPasscode action][GRAPH-1]

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-AC2]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/DeviceActionList.ReactView
[INT-1]:/intune/device-configuration/settings-catalog/ref-android-settings

[INT-RC]: ../../fundamentals/role-based-access-control/create-custom-role.md
[INT-R1]: ../../fundamentals/role-based-access-control/ref-built-in-roles.md#help-desk-operator
[INT-R2]: ../../fundamentals/role-based-access-control/ref-built-in-roles.md#school-administrator

[GRAPH-1]: /graph/api/intune-devices-manageddevice-resetpasscode
