---
title: "Intune Remote Device Action: Restart"
description: Learn how to restart managed devices with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management

zone_pivot_groups: c5fbc3ee-cfe5-494a-b441-d95cbed3128c
---

# Remotely restart devices using Intune

The **Restart** remote action triggers a restart (usually begins within 5 minutes) and might not show a warning to the signed-in user.

> [!IMPORTANT]
> The restart depends on the device receiving a push notification. If the device is offline or push notifications are blocked, the restart is delayed until connectivity resumes.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)
> - Android Open Source Project (AOSP)
> - iOS/iPadOS in [Supervised Mode][IOS-SUP]
> - macOS
> - Windows
> - ChromeOS

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Reboot now**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## Restart a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Restart** > **Yes**.

::: zone pivot="windows,ios"
## User experience
::: zone-end

::: zone pivot="ios"
A passcode-locked device can't reconnect to Wi-Fi until the user unlocks it. Apple encrypts saved Wi-Fi credentials until unlock. Until then, Intune can't communicate with the device.
::: zone-end

::: zone pivot="windows"
When the 5‑minute restart timer starts, Windows attempts to show the notification: *Your device administrator has scheduled a reboot.* Delivering the restart command requires Windows Notification Services (WNS).

For more information about WNS, see [Network endpoint requirements](../fundamentals/intune-endpoints.md#windows-push-notification-services-wns-dependencies).
::: zone-end

## Reference links

::: zone pivot="windows"
- Configuration service provider (CSP) used to initiate the remote action: [Reboot CSP][CSP-1]
::: zone-end
- Microsoft Graph API: [rebootNow action][GRAPH-1]

<!--links-->

<!-- graph -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rebootnow

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- roles -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

[IOS-SUP]: /intune/intune-service/remote-actions/device-supervised-mode

[CSP-1]: /windows/client-management/mdm/reboot-csp

::: zone pivot="windows,ios,macos,android,chrome"
::: zone-end
