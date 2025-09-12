---
title: "Intune Remote Device Action: Rotate local admin password"
description: Learn how to rotate the local admin password on Windows and macOS devices with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri

zone_pivot_groups: 2fce401c-16eb-4314-8d26-844d8612f9c5
---

# Rotate local admin password using Intune

The **Rotate local admin password** remote action in Microsoft Intune allows to manually rotate the password of a device's local administrator account. This action helps improve security by ensuring that credentials are refreshed outside of the scheduled rotation defined by Windows LAPS policies. It's especially useful when responding to potential compromise, performing audits, or resetting access for support scenarios.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
> - macOS [enrolled via Automated Device Enrollment (ADE)][MAC-ADE]
> - Windows (corporate-owned)

### :::image type="icon" source="../media/icons/headers/config.svg" border="false"::: Device configuration

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

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Rotate Local Admin Password**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to rotate the local admin password from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Rotate Local admin password**.

## Reference links

- Microsoft Graph API: [rotatelocaladminpassword action][GRAPH-1]
- Configuration service provider (CSP) used to initiate the remote action: [LAPS CSP][CSP-1]

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