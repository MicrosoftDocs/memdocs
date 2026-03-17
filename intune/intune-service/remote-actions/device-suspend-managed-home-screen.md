---
title: "Remote Device Action: Suspend Managed Home Screen"
description: Learn how to suspend the Managed Home Screen with Microsoft Intune.
ms.date: 01/20/2026
ms.topic: how-to
---

# Remote device action: suspend Managed Home Screen

The *suspend Managed Home Screen* remote action in Intune temporarily disables the Managed Home Screen on a device. When the Managed Home Screen is suspended, the device will no longer enforce the Managed Home Screen policies, and the user will have access to the standard home screen and apps.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)

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
>   - The permission **Remote tasks/Temporarily Suspend Managed Home Screen**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> To run this remote action, the **Alarms & Reminders** permission must be granted to the Managed Home Screen.
>
> For more information, see [Configure permissions for the Managed Home Screen (MHS) on Android Enterprise devices using Microsoft Intune](../configuration/oemconfig-managed-home-screen-permissions-android.md).

:::column-end:::
:::row-end:::

## How to suspend the managed home screen from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Suspend Managed Home Screen**.

## User experience

Once the Managed Home Screen is suspended, the device will no longer enforce the Managed Home Screen policies, and the user will have access to the standard home screen and apps.

## Reference links

- Microsoft Graph API: [managedDevice resource type][GRAPH-1]
<!--
- Microsoft Graph API: [temporarilySuspendManagedHomeScreen action][GRAPH-2]
-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/resources/intune-devices-manageddevice
[GRAPH-2]: /graph/api/intune-devices-manageddevice-TemporarilySuspendManagedHomeScreen
