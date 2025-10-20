---
title: "Remote Device Action: Remove Passcode"
description: Learn how to remove a passcode with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
---

# Remote device action: remove passcode

With the *remove passcode* action in Microsoft Intune, you can remotely remove a device passcode to help users regain access to their devices without requiring a full device wipe. This remote action is especially useful when a user forgets their passcode or is locked out of their device.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - iOS/iPadOS (corporate-owned)

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote Tasks/Reset Passcode**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)


## How to remove a passcode from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Remove passcode**.

## User experience

Once the passcode is removed, if there's a passcode policy set, the device prompts the user to set a new passcode in Settings.

> [!IMPORTANT]
> If the Remove passcode action fails, Intune might have stored the wrong unlock token, and you need to **Wipe** the device to regain access.

## Reference links

- Microsoft Graph API: [resetPasscode action][GRAPH-1]

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-AC2]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/DeviceActionList.ReactView
[INT-1]:/intune/intune-service/configuration/settings-catalog-android

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/intune-devices-manageddevice-resetpasscode
