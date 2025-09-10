---
title: "Intune Remote Device Action: Autopilot Reset"
description: Learn how to use Autopilot reset with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri

zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Autopilot reset using Intune

[Link](/autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)

Exec on this node triggers Autopilot Reset operation. This works like PC Reset, similar to other existing nodes in this RemoteWipe CSP, except that it keeps the device enrolled in Microsoft Entra ID and MDM, keeps Wi-Fi profiles, and a few other settings like region, language, keyboard.

<div data-bind="&quot;text&quot;:data.text" class="fxs-messagebox-text" id="messagebox0-000">Windows Autopilot Reset quickly removes personal files, apps, and settings. It resets devices running Windows 10 and later from the lock screen, and applies original management settings from Microsoft Entra ID and Intune device management. This returns the device to a fully configured or known IT-approved state. (If an enrollment status page wasn't configured for this device during initial device enrollment, the device will go straight to the desktop after sign-in. It might take up to eight hours to sync and appear compliant in Intune.)</div>

From portal:

/wipe
{keepUserData: "false", keepEnrollmentData: "true"}

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Windows

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

🤔

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Wipe**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

### How to use Autopilot reset from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Autopilot reset**.
1. To confirm, select **Yes**.

## Reference links

- Configuration service provider (CSP) used to initiate the remote action: [RemoteWipe CSP][CSP-1]
- Microsoft Graph API: [wipe action][GRAPH-1]

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

[GRAPH-1]: /graph/api/intune-devices-manageddevice-wipe
[CSP-1]: /windows/client-management/mdm/remotewipe-csp