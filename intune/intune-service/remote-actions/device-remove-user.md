---
title: "Remote Device Action: Remove User"
description: Learn how to remove a user from a Shared iPad with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
---

# Remote device action: remove user

The *remove user* remote device action in Microsoft Intune deletes a selected user's cached session from a Shared iPad. This helps free up storage, support privacy, and prepare the iPad for other users. The removed user can sign in again if needed.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action is supported on the following platform:
>
> - iPadOS (Shared iPad mode only)

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Manage shared device users**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to remove a user from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a Shared iPadOS device.
1. Select **Users**.
1. In the list, right-click the user that you want to remove, and then select **Remove user**.

## Reference links

- Microsoft Graph API: [deleteUserFromSharedAppleDevice action][GRAPH-1]

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[GRAPH-1]: /graph/api/intune-devices-manageddevice-deleteuserfromsharedappledevice
