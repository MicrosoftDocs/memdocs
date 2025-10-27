---
title: "Remote Device Action: Logout current user"
description: Learn how to use the logout the current user from a Shared iPad with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Remote device action: logout current user

The *logout current user* remote device action in Microsoft Intune allows IT administrators to remotely sign out the active user from a Shared iPad.
This remote action is useful in environments where multiple users access the same device throughout the day. Logging out the current user helps maintain privacy, ensures session cleanup, and prepares the device for the next user—supporting secure and efficient device turnover in shared-use scenarios.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action is supported on the following platform:
>
> - iPadOS (Shared iPad mode only)

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Manage shared device users**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to logout the current user from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Logout current user**.

## Reference links

- Microsoft Graph API: [logoutSharedAppleDeviceActiveUser action][GRAPH-1]

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[GRAPH-1]: /graph/api/intune-devices-manageddevice-logoutsharedappledeviceactiveuser
