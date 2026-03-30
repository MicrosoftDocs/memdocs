---
title: "Remote Device Action: Rotate Recovery Lock Passcode"
description: Learn how to rotate the macOS Recovery Lock passcode with Microsoft Intune.
ms.date: 03/09/2026
ms.topic: how-to
---

# Remote Device Action: rotate Recovery Lock passcode

<!-- Remove this note after rollout completes (target: late April 2026) -->
> [!NOTE]
> This feature is gradually rolling out and may not yet be available in your tenant. Full availability is expected by late April 2026.

Recovery Lock protects macOS devices by requiring a password to access recoveryOS. By using Intune, administrators can remotely rotate this passcode to keep access to the recovery environment secure and controlled.

When you use the **Rotate Recovery Lock Passcode** action, Intune creates a new passcode to replace the current one. The new passcode shows up in the admin center and is the only valid credential for accessing the device's recovery options.

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
1. Select **Yes** to confirm the action. Intune generates a new Recovery Lock passcode.

> [!NOTE]
> Confirming this action starts the passcode rotation process.  
> The new Recovery Lock passcode is applied to the device the next time the device successfully checks in with Intune.  
> If the device is offline or not checking in, the existing Recovery Lock passcode remains in effect until the device checks in.

To view the new passcode, select **Passwords and keys** > **View Recovery Lock Passcode**.

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

