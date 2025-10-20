---
title: "Remote Device Action: Reset Passcode"
description: Learn how to reset a passcode with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
---

# Remote device action: reset passcode

With the *reset passcode* action in Microsoft Intune, you can remotely reset a device passcode to help users regain access to their devices without requiring a full device wipe. This remote action is especially useful when a user forgets their passcode or is locked out of their device or work profile.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
> - Android Enterprise personally-owned work profile (BYOD)
> - Android Open Source Project (AOSP)

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote Tasks/Reset Passcode**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## Passcode reset types

When working with Android devices, it's important to understand the two types of passcode resets available:

- **Device-level passcode reset**: The action resets the passcode for the entire device.
- **Work profile passcode reset**: The action resets the passcode for the user's work profile only.

The following table summarizes the passcode reset types based on platform:

| Platform | Device-level passcode reset | Work profile passcode reset |
|--|:-:|:-:|
| Android Enterprise corporate-owned dedicated (COSU) | ✅ | ❌ |
| Android Enterprise corporate-owned fully managed (COBO) | ❌ | ✅ |
| Android Enterprise corporate-owned work profile (COPE) | ❌ | ✅ |
| Android Enterprise personally-owned work profile (BYOD) | ❌ | ✅ |
| Android Open Source Project (AOSP) | ✅ | ❌ |

> [!IMPORTANT]
> Before initiating a passcode reset, ensure that the passcode requirement is enforced via [device configuration policies][INT-1]—otherwise, the reset fails.

## How to reset a passcode from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Reset passcode**.
1. A new passcode is presented to the admin.

The new passcode must be entered on the device, and it's displayed in the admin center for seven days.

## User experience

For work profile passcode reset, users get notified to activate their reset passcode. After their passcode is entered, the notification is dismissed.

>[!NOTE]
>If the remote lock action fails, confirm that you have a device passcode policy assigned to the device. If the device doesn't have a device passcode assigned, the remote lock action doesn't succeed.

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
