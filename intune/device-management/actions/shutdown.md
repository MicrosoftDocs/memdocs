---
title: "Device Action: Shutdown"
description: Learn how to shutdown Apple devices with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: shut down

With the *shut down* action, IT administrators can remotely power off managed devices. This action doesn't prompt or warn the user before the device powers down.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
>
> - iOS/iPadOS in [Supervised Mode][IOS-SUP]
> - macOS

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
> - [School Administrator]
> - [Endpoint Security Manager]
> - [Custom role] that includes:
>   - The permission **Remote tasks/Shut down**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to shut down a device from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Shut down** > **Yes**.

> [!NOTE]
> iOS/iPadOS devices that are Passcode-locked will not rejoin a Wi-Fi network after restarting. After restarting, the device might not be able to communicate with the server.

## Reference links

- Microsoft Graph API: [shutDown action][GRAPH-1]

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!--Role links-->

[ENT-R1]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator
[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#help-desk-operator
[School Administrator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#school-administrator
[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role
[Endpoint Security Manager]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#endpoint-security-manager

<!--Graph API links-->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-shutdown

<!--Other links-->

[IOS-SUP]: /intune/intune-service/remote-actions/device-supervised-mode
