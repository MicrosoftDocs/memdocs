---
title: "Remote Device Action: Rotate Recovery Lock Passcode"
description: Learn how to rotate the macOS Recovery Lock passcode with Microsoft Intune.
ms.date: 03/09/2026
ms.topic: how-to
---

# Remote Device Action: rotate Recovery Lock passcode

The *rotate Recovery Lock passcode* remote action in Intune allows administrators to rotate the Recovery Lock passcode for a managed macOS device. The Recovery Lock password is used to unlock a macOS device that has been locked due to too many failed login attempts or other security reasons. By rotating the Recovery Lock passcode, administrators can ensure that they have access to the device if it becomes locked, while also maintaining security by regularly changing the passcode. When this action is performed, a new Recovery Lock passcode will be generated and displayed in the Intune admin center, allowing the administrator to use it for device recovery if needed.

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
> - Intune administrator
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks / Rotate macOS Recovery Lock password**
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

## How to rotate the macOS Recovery Lock passcode from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Rotate Recovery Lock Passcode**.
1. Select **Yes** to confirm the action. A new Recovery Lock Passcode will be generated.

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

