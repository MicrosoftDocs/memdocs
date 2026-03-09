---
title: "Remote Device Action: Rotate Recovery Lock Passcode"
description: Learn how to rotate the macOS Recovery Lock passcode with Microsoft Intune.
ms.date: 03/09/2026
ms.topic: how-to
---

# Remote Device Action: rotate Recovery Lock passcode

Recovery Lock protects macOS devices by requiring a password to access recoveryOS. With Intune, administrators can remotely rotate this passcode to maintain secure, controlled access to the recovery environment.

Using the **Rotate Recovery Lock Passcode** action, Intune generates a new passcode that replaces the existing one. The updated passcode appears in the admin center and becomes the only valid credential for accessing the device's recovery options.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
> - macOS in supervised mode, running macOS 11.5 or later on Apple silicon (Intel-based Macs aren't supported).

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
> To run this remote action, the device must be configured with a policy setting that enables the Recovery Lock feature.
>
> For more information, see [Create the Recovery Lock policy](../configuration/settings-catalog-recovery-lock.md#create-the-recovery-lock-policy).

:::column-end:::
:::row-end:::

## How to rotate the macOS Recovery Lock passcode from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Rotate Recovery Lock Passcode**.
1. Select **Yes** to confirm the action. A new Recovery Lock Passcode will be generated.
   - To view the new passcode, select **Passwords and keys** > **View Recovery Lock Passcode**.

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

