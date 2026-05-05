---
title: "Device Action: Run Remediation"
description: Learn how to initiate on demand remediations with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: run remediation

The *run remediation* action in Microsoft Intune allows IT administrators to proactively detect and resolve support issues on managed devices. This action triggers a remediation script that checks for specific conditions and applies a fix if needed—without requiring user interaction.

Use this action to address common problems such as configuration drift, missing settings, or compliance gaps. It's especially useful for maintaining device health across large environments.

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
> - [School Administrator]
> - [Custom role] that includes:
>   - The permission **Remote tasks/Run Remediation**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to run a remediation from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Run remediation (preview)**.
1. In the **Run remediation (preview)** pane, select the Script package you want to run from the list.
1. To run the remediation, select **Run remediation**.

To learn more about remediations in Microsoft Intune—including what they are, along with prerequisites and licensing requirements—see [Use Remediations to detect and fix support issues][LEARN-1].

## Reference links

- Microsoft Graph API: [initiateOnDemandProactiveRemediation action][GRAPH-1]

<!--links-->

<!-- admin center links -->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!-- role links -->

[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#help-desk-operator
[School Administrator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#school-administrator
[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role.md

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-initiateondemandproactiveremediation

[LEARN-1]: ../tools/deploy-remediations.md
