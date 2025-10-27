---
title: "Remote Device Action: Sync"
description: Learn how to use the device sync remote action in Intune to apply policy, app, and configuration updates to managed devices.
ms.date: 10/27/2025
ms.topic: how-to
zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Remote device action: sync

The *sync* device action forces a device to check in with Intune. When a device checks in, it receives any pending actions or policies assigned to it. This action is useful for validating and troubleshooting policy deployment without waiting for the next scheduled check-in.

For more information about the standard Intune policy check-in frequencies, see [Refresh cycle times](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action is supported on the following platform:
> - Android
> - iOS/iPadOS
> - macOS
> - Windows

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Sync devices**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to sync a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Sync**.
1. To confirm, select **Yes**.

::: zone pivot="ios,android"

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

::: zone-end

## Reference links

- Microsoft Graph API: [syncDevice action][GRAPH-1]


[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager

[GRAPH-1]: /graph/api/intune-devices-manageddevice-syncdevice

::: zone pivot="windows,ios,macos,android"
::: zone-end
