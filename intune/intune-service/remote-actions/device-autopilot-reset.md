---
title: "Remote Device Action: Autopilot Reset"
description: Learn how to use Autopilot reset with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri

titleSuffix: Microsoft Intune 1
---

# Remote device action: Autopilot Reset


Use the *Autopilot Reset* remote action in Intune to prepare a Windows device for reuse while maintaining its Microsoft Entra ID and Intune enrollment. Autopilot Reset removes user data, settings, and apps, and reapplies the original device configuration.

The reset preserves key settings, including Wi-Fi profiles and credentials, allowing the device to reconnect automatically after the reset. Region, language, and keyboard settings are also retained.

Autopilot Reset is designed for scenarios where a device needs to be repurposed or reassigned. It returns the device to a fully configured, IT-approved state without requiring a full reimage.

For more information, see [Windows Autopilot Reset](/autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset).

## Requirements

[!INCLUDE [platform-requirements](../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - Windows

[!INCLUDE [rbac-requirements](../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Wipe**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

### How to use Autopilot reset from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Autopilot reset**.
1. To confirm, select **Yes**.

## Reference links

- Configuration service provider (CSP) used to initiate the remote action: [RemoteWipe CSP][CSP-1]
- Microsoft Graph API: [wipe action][GRAPH-1]

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

[GRAPH-1]: /graph/api/intune-devices-manageddevice-wipe
[CSP-1]: /windows/client-management/mdm/remotewipe-csp