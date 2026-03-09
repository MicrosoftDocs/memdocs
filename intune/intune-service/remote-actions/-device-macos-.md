---
title: "Remote Device Action: View macOS Recovery Lock Password"
description: Learn how view the macOS recovery lock password with Microsoft Intune.
ms.date: 03/09/2026
ms.topic: how-to
---

# Remote Device Action: view macOS recovery lock password"

The *view macOS recovery lock password* remote action in Intune allows administrators to view the recovery lock password for a managed macOS device. The recovery lock password is used to unlock a macOS device that has been locked due to too many failed login attempts or other security reasons. By viewing the recovery lock password, administrators can provide it to users to help them regain access to their locked devices.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
> - macOS

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks / Rotate macOS recovery lock password** and **Remote tasks / View macOS recovery lock password**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> To run this remote action, the 

:::column-end:::
:::row-end:::

## How to view the macOS recovery lock password from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Add here**.

## Reference links

- Microsoft Graph API: [managedDevice resource type][GRAPH-1]
<!--
- Microsoft Graph API: [restoreManagedHomeScreen action][GRAPH-2]
-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/resources/intune-devices-manageddevice
[GRAPH-2]: /graph/api/intune-devices-manageddevice-RestoreManagedHomeScreen

