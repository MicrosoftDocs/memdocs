---
title: "Remote Device Action: Run Remediation"
description: Learn how to initiate on demand remediations with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
---

# Remote device action: run remediation

The *run remediation* remote action in Microsoft Intune allows IT administrators to proactively detect and resolve support issues on managed devices. This action triggers a remediation script that checks for specific conditions and applies a fix if needed—without requiring user interaction.

Use this action to address common problems such as configuration drift, missing settings, or compliance gaps. It's especially useful for maintaining device health across large environments.

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
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Run Remediation**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to run a remediation from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Run remediation (preview)**.
1. In the **Run remediation (preview)** pane, select the Script package you want to run from the list.
1. To run the remediation, select **Run remediation**.

To learn more about remediations in Microsoft Intune—including what they are, along with prerequisites and licensing requirements—see [Use Remediations to detect and fix support issues][LEARN-1].

## Reference links

- Microsoft Graph API: [initiateOnDemandProactiveRemediation action][GRAPH-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-initiateondemandproactiveremediation

[LEARN-1]: ../fundamentals/remediations.md
