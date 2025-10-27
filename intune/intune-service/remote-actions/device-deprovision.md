---
title: "Intune Remote Action: Deprovision"
description: Learn how to deprovision a chromeOS device with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Remote device action: deprovision

The *deprovision* device action in Microsoft Intune enables IT administrators to remove Google Admin policies from ChromeOS devices that are no longer in use by the organization.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
>
> - ChromeOS

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
>   - The permission **Remote tasks/Retire**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::

## How to deprovision a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Deprovision**. To confirm, select **Yes**.

After you deprovision a device, it remains in the Intune admin center and the Google Admin console. In the **System info** pane, the device status changes to **Deprovisioned**. The device can't be enrolled again until you restore it to factory settings. For more information about the deprovision action, such as how to select the best reason for deprovisioning, see the [Chrome Enterprise and Education Help documentation](https://support.google.com/chrome/a/answer/3523633?).

## Reference links

- Microsoft Graph API: [deprovision action][GRAPH-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-deprovision