---
# required metadata

title: Remove a User From an iPadOS Device With Microsoft Intune
titleSuffix:
description: Learn how to remove a user from a shared iOS/iPadOS device with Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Remove a user from a shared iOS/iPadOS device

The **Remove user** action deletes a user that you select from the local cache on a shared iPad device.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platform:
>
> - iPadOS (shared iPad devices only)

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Custom role][INT-RC] with the permission:
>   - Remote tasks/Manage shared device users

## Remove a user

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From the devices list, select a shared iPadOS device.
1. Select **Users**.
1. In the list, right-click the user that you want to remove, and then select **Remove user**.

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [deleteUserFromSharedAppleDevice action][GRAPH-1].

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[GRAPH-1]: /graph/api/intune-devices-manageddevice-deleteuserfromsharedappledevice
