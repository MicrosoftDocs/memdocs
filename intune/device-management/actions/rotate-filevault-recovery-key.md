---
title: "Device Action: Rotate FileVault Recovery Key"
description: Learn how to rotate the FileVault recovery key with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: rotate FileVault recovery key

The *rotate FileVault recovery key* action in Microsoft Intune allows IT admins to manually generate a new personal recovery key for a macOS device encrypted with FileVault.

This action is useful when the current key is lost, potentially exposed, or needs to be refreshed for compliance or support reasons.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
>
> - macOS (corporate-owned)
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> To use this action, make sure devices meet the following requirements:
>
> - Are encrypted with FileVault using an Intune disk encryption policy.
> - Have the FileVault recovery key escrowed to Intune.
>
> For more information, see Use [FileVault disk encryption for macOS with Intune][LEARN-1].

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
> - [Endpoint Security Manager]
> - [Custom role] that includes:
>   - The permission **Remote tasks/Rotate filevault key**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to rotate the FileVault recovery key from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Rotate FileVault recovery key**.
1. Select **Yes** to confirm the action.

## Reference links

- Microsoft Graph API: [rotateFileVaultKey action][GRAPH-1]

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!--Role links-->

[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#help-desk-operator
[Endpoint Security Manager]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#endpoint-security-manager
[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role

<!--Graph API links-->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotateFileVaultKey

<!--Other links-->

[LEARN-1]: ../../device-configuration/endpoint-security/encrypt-filevault-macos.md
