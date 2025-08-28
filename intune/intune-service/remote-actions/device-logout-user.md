---
# required metadata

title: Log out the user of an iOS/iPadOS device
description: Learn how to log out the current user of an iOS/iPadOS device with Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Sign out the current user

The **Logout current user** action logs out the current user on a shared iPad device.

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
> - [Custom role][INT-RC] that includes:
>   - The permission: **Remote tasks/Manage shared device users**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Read device, Update devices)

## Log out the current user

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**](https://go.microsoft.com/fwlink/?linkid=2333814)
1. From the devices list, select a device, and then select **...** > **Logout current user**.

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [logoutSharedAppleDeviceActiveUser action][GRAPH-1].

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[GRAPH-1]: /graph/api/intune-devices-manageddevice-logoutsharedappledeviceactiveuser
