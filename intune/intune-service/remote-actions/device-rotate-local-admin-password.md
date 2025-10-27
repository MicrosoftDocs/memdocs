---
title: "Remote Device Action: Rotate local admin password"
description: Learn how to rotate the local admin password on Windows and macOS devices with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
zone_pivot_groups: 2fce401c-16eb-4314-8d26-844d8612f9c5
---

# Remote device action: rotate local admin password

The *rotate local admin password* remote action in Microsoft Intune lets IT admins manually rotate the password of a device's local administrator account. This helps improve security by refreshing credentials outside the scheduled rotation defined by the Microsoft Local Administrator Password Solution (LAPS). It's especially useful when responding to potential compromise, conducting audits, or resetting access during support scenarios.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
> - macOS [enrolled via Automated Device Enrollment (ADE)][MAC-ADE]
> - Windows (corporate-owned)

[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

::: zone pivot="windows"

> [!div class="checklist"]
> To use this remote action, make sure devices meet the following requirements:
>
> - Are Microsoft Entra joined or Hybrid Entra joined.
> - Have Windows LAPS configured and actively backing up the local admin password to Microsoft Entra ID.

For more information, see [What is Windows LAPS?][LEARN-1].

::: zone-end

::: zone pivot="macos"

> [!div class="checklist"]
> To use this remote action, make sure devices meet the following requirements:
>
> - The local admin account must be configured in the ADE profile before enrollment.

For more information, see [Configure support for macOS ADE local account with LAPS][LEARN-2].

::: zone-end

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

> To run this remote action, use an account with at least one of the following roles:
>
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Rotate Local Admin Password**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to rotate the local admin password from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Rotate Local admin password**.

## Reference links

- Microsoft Graph API: [rotatelocaladminpassword action][GRAPH-1]
::: zone pivot="windows"
- Configuration service provider (CSP) used to initiate the remote action: [LAPS CSP][CSP-1]
::: zone-end

<!--links-->

[more info](../protect/windows-laps-policy.md#manually-rotate-passwords)

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->


[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotatelocaladminpassword
[CSP-1]: /windows/client-management/mdm/laps-csp

[LEARN-1]: /windows-server/identity/laps/laps-overview
[LEARN-2]: /intune/intune-service/enrollment/macos-laps
[MAC-ADE]: /intune/intune-service/enrollment/device-enrollment-program-enroll-macos