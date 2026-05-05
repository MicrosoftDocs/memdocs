---
title: "Device Action: Full Scan"
description: Learn how to initiate on demand Microsoft Defender full scan with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: full scan

The *full scan* action in Intune lets IT admins trigger a comprehensive malware scan on managed Windows devices using Microsoft Defender Antivirus. It checks all files and running processes, helping detect threats missed by quick scans.

This action is ideal when a device is suspected of compromise or when validating security baselines. Instead of waiting for scheduled scans or relying on user action, admins can launch a full scan directly from the Intune admin center.

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
>   - The permission **Remote tasks/Windows defender**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to initiate a full scan from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Full scan**.

## Reference links

- Microsoft Graph API: [windowsDefenderScan action][GRAPH-1]
- Configuration service provider (CSP) used to initiate the action: [Defender CSP][CSP-1]

<!--links-->

<!-- admin center links -->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!-- role links -->

[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#help-desk-operator
[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role.md
[Endpoint Security Manager]: /intune/fundamentals/role-based-access-control/ref-built-in-roles.md#endpoint-security-manager

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-windowsdefenderscan

[CSP-1]: /windows/client-management/mdm/defender-csp
