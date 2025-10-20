---
title: "Remote Device Action: Remote Lock"
description: Use the remote lock action in Microsoft Intune to lock a managed device that has a passcode or PIN.
ms.date: 09/22/2025
ms.topic: how-to
zone_pivot_groups: bf632d5b-6209-46d2-8c9c-8d76b1f704cc
---

# Remote device action: remote lock

The *remote lock* device action locks a managed device so the user must enter the existing passcode or PIN to continue. Use this action when a device is misplaced, left unattended, or suspected of unauthorized use without wiping data or removing enrollment.

> [!IMPORTANT]
> Remote lock is only effective if a passcode or PIN is already set:
> - If no passcode exists, the screen may just turn off and the user can still access the device.
> - Enforce a passcode policy before relying on this action.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
> - Android Open Source Project (AOSP)
> - iOS/iPadOS
> - macOS

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Remote lock**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to remote lock a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Remote lock**.
::: zone pivot="macos"
3. Set a six-digit recovery PIN.

> [!NOTE]
> The recovery PIN is shown on the device overview pane for up to 30 days, or until another device action is sent. Record it securely; it can't be retrieved afterward. Don't resend remote lock to the same macOS device until that PIN is used—additional attempts show a **Failed** status in reporting.

::: zone-end
::: zone pivot="ios,android"
::: zone-end

## Reference links

- Microsoft Graph API: [remoteLock action][GRAPH-1]

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-remotelock
