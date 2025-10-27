---
title: "Intune Remote Action: Rotate FileVault Recovery Key"
description: Learn how to rotate the FileVault recovery key with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Remote device action: rotate FileVault recovery key

The *rotate FileVault recovery key* remote action in Microsoft Intune allows IT admins to manually generate a new personal recovery key for a macOS device encrypted with FileVault.

This action is useful when the current key is lost, potentially exposed, or needs to be refreshed for compliance or support reasons.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
>
> - macOS (corporate-owned)
:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> To use this remote action, make sure devices meet the following requirements:
>
> - Are encrypted with FileVault using an Intune disk encryption policy.
> - Have the FileVaultpersonal recovery key escrowed to Intune.

For more information, see Use [FileVault disk encryption for macOS with Intune][LEARN-1].

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
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Rotate filevault key**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to rotate BitLocker keys from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Rotate FileVault recovery key**.
1. Select **Yes** to confirm the action.

## Reference links

- Microsoft Graph API: [rotateFileVaultKey action][GRAPH-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotateFileVaultKey

[LEARN-1]: /intune/intune-service/protect/encrypt-devices-filevault
