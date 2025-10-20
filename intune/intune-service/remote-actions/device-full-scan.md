---
title: "Remote Device Action: Full Scan"
description: Learn how to initiate on demand Microsoft Defender full scan with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
---

# Remote device action: full scan

The *full scan* remote action in Intune lets IT admins trigger a comprehensive malware scan on managed Windows devices using Microsoft Defender Antivirus. It checks all files and running processes, helping detect threats missed by quick scans.

This action is ideal when a device is suspected of compromise or when validating security baselines. Instead of waiting for scheduled scans or relying on user action, admins can launch a full scan directly from the Intune admin center.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - Windows

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Windows defender**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to initiate a full scan from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Full scan**.

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
