---
title: "Device Action: Remove User"
description: Learn how to remove a user from a Shared iPad with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: remove user

The *remove user* device action in Microsoft Intune deletes a selected user's cached session from a Shared iPad. This helps free up storage, support privacy, and prepare the iPad for other users. The removed user can sign in again if needed.

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
## How to remove a user from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a Shared iPadOS device.
1. Select **Users**.
1. In the list, right-click the user that you want to remove, and then select **Remove user**.

## Reference links

- Microsoft Graph API: [deleteUserFromSharedAppleDevice action][GRAPH-1]

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!--Role links-->

[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role
[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#help-desk-operator
[School Administrator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#school-administrator

<!--Graph API links-->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-deleteuserfromsharedappledevice
