---
title: "Intune Remote Actions: Full Scan"
description: Learn how to initiate on demand Microsoft Defender full scan with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Full scan with Microsoft Defender in Intune

The **Full Scan** remote action in Microsoft Intune allows IT administrators to initiate a comprehensive malware scan on managed Windows devices using Microsoft Defender Antivirus. This action triggers a full system scan that checks all files and running programs, helping to detect and remediate threats that may not be caught during routine quick scans.
This capability is especially useful in scenarios where a device is suspected of being compromised, or when you need to validate that security baselines and threat protection policies are functioning as expected. Instead of waiting for the next scheduled scan or relying on user-initiated actions, you can proactively launch a full scan directly from the Intune admin center—ensuring faster response and greater control.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Windows

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute these remote actions, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Windows defender**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to initiate a full scan

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **...** > **Full scan**.

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
