---
title: "Remote Device Action: Quick Scan"
description: Learn how to initiate on demand Microsoft Defender quick scan with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Remote device action: quick scan

The *quick scan* remote action in Microsoft Intune enables IT administrators to start a targeted malware scan on managed Windows devices by using Microsoft Defender Antivirus. This action scans key system areas where threats commonly appear—such as memory, startup folders, and running processes—without performing a full system sweep.

Quick scans are especially useful for routine health checks, validating recent policy deployments, or responding to low-risk alerts. By triggering a scan remotely from the Intune admin center, IT teams can quickly assess device health and ensure protection is up to date—without waiting for the next scheduled scan or relying on user intervention.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platform:
>
> - Windows

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Windows defender**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to initiate a quick scan from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Quick scan**.

## Reference links

- Microsoft Graph API: [windowsDefenderScan action][GRAPH-1]
- Configuration service provider (CSP) used to initiate the remote action: [Defender CSP][CSP-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-windowsdefenderscan

[CSP-1]: /windows/client-management/mdm/defender-csp
