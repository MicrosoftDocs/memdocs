---
title: "Device Action: BitLocker Key Rotation"
description: Learn how to rotate the BitLocker recovery key with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: BitLocker key rotation

The *BitLocker key rotation* action in Microsoft Intune lets IT admins remotely refresh the recovery key for the operating system drive on BitLocker-encrypted Windows devices. This helps reduce the risk of unauthorized access if a recovery key has been used or potentially exposed.

Key rotation is especially useful in environments where devices are frequently serviced, reassigned, or exposed to support scenarios. For example, if a helpdesk technician shares a recovery key during a support call, you can rotate the key from Intune to ensure it can't be reused.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
>
> - Windows

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
>   - The permission **Remote tasks/Rotate BitLockerKeys**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to rotate the BitLocker key from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **BitLocker key rotation**.
1. Select **Yes** to confirm the action.

## Reference links

- Configuration service provider (CSP) used to initiate the action: [BitLocker CSP][CSP-1]
- Microsoft Graph API: [rotateBitLockerKeys action][GRAPH-1]
- [BitLocker overview][WIN-1]

<!--links-->

<!-- admin center links -->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!-- role links -->

[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#help-desk-operator
[Endpoint Security Manager]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#endpoint-security-manager
[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role.md

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotateBitLockerKeys


<!-- MSLearn links -->

[WIN-1]: /windows/security/operating-system-security/data-protection/bitlocker/
[CSP-1]: /windows/client-management/mdm/bitlocker-csp#rotaterecoverypasswords
