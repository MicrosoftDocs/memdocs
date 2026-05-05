---
title: "Device Action: Logout Current User"
description: Learn how to use the logout the current user from a Shared iPad with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: logout current user

The *logout current user* device action in Microsoft Intune allows IT administrators to remotely sign out the active user from a Shared iPad.
this action is useful in environments where multiple users access the same device throughout the day. Logging out the current user helps maintain privacy, ensures session cleanup, and prepares the device for the next user—supporting secure and efficient device turnover in shared-use scenarios.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
>
> - iPadOS (Shared iPad mode only)

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this action, use an account with at least one of the following roles:
>
> - [Help Desk Operator]
> - [Custom role] that includes:
>   - The permission **Remote tasks/Manage shared device users**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to logout the current user from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Logout current user**.

## Reference links

- Microsoft Graph API: [logoutSharedAppleDeviceActiveUser action][GRAPH-1]

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role.md
[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#help-desk-operator
[School Administrator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#school-administrator
[GRAPH-1]: /graph/api/intune-devices-manageddevice-logoutsharedappledeviceactiveuser
