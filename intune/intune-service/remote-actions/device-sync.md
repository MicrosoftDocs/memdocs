---
# required metadata

title: "Intune Remote Device Action: Sync"
description: Learn how to use the device sync remote action in Intune to immediately apply policy, app, and configuration updates to managed devices.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Sync devices to get the latest policies and actions with Intune

The **Sync** device action forces the selected device to immediately check in with Intune. When a device checks in, it immediately receives any pending actions or policies assigned to it. This feature can help you immediately validate and troubleshoot policies you're assigned to, without waiting for the next scheduled check-in.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platform:
>
> - Android
> - iOS/iPadOS
> - macOS
> - Windows

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] with the permissions:
>   - Remote tasks/Sync devices

## How to sync a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From the devices list, select a device, and then select **Sync**.
1. To confirm, select **Yes**.

You can find standard Intune policy check-in frequencies in the [Refresh cycle times](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

## Retryable error codes

When you execute the **Sync** remote action, iOS/iPadOS and Android apps that failed and raised a retryable error code are still available to the device. However, apps that raised a nonretryable error code must wait seven days before they're available to the device.

| Error code  | Suggested description | Retryable |
|---|---|---|
| 2016330898 | An unknown error occurred. | No |
| 2016330897 | Your connection to Intune timed out. Reset your connection. | Yes |
| 2016330896 | You lost connection to the Internet. Reset your connection. | Yes |
| 2016330895 | You lost connection to the Internet. Reset your connection. | Yes |
| 2016330894 | You lost connection to the Internet. Reset your connection. | Yes |
| 2016330893 | You lost connection to the Internet. Reset your connection. | Yes|
| 2016330892 | International roaming is disabled. | No|
| 2016330891 | The cellular data connection for this device can't be accessed while a phone call is being made. Wait for the phone call to complete. | Yes|
| 2016330890 | The cellular network for this device. These devices couldn't be used at this time. | No|
| 2016330889 | The secure connection failed. Reset your connection. | Yes|
| 2016330888 | The server trust evaluation has failed. | No|

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [syncDevice action][GRAPH-1].


[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager

[GRAPH-1]: /graph/api/intune-devices-manageddevice-syncdevice
