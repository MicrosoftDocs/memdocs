---
title: "Device Action: Restart"
description: Learn how to restart managed devices with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
zone_pivot_groups: c5fbc3ee-cfe5-494a-b441-d95cbed3128c
---

# Device action: restart

The *restart* action triggers a restart (usually begins within 5 minutes) and might not show a warning to the signed-in user.

> [!IMPORTANT]
> The restart depends on the device receiving a push notification. If the device is offline or push notifications are blocked, the restart is delayed until connectivity resumes.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)
> - Android Open Source Project (AOSP)
> - iOS/iPadOS in [Supervised Mode][IOS-SUP]
> - macOS
> - Windows
> - ChromeOS (kiosk mode or managed guest session)

::: zone pivot="chromeos"

> [!NOTE]
> Restart is only available for kiosk devices and managed guest session devices. The restart fails on any other type of device. For more information, see [Kiosk apps, managed guest sessions, and smart cards](https://support.google.com/chrome/a/topic/6128720?) (opens Google Chrome Enterprise Help).
::: zone-end

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Reboot now**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to restart a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Restart** > **Yes**.

::: zone pivot="windows,ios"
## User experience
::: zone-end

::: zone pivot="ios"
A passcode-locked device can't reconnect to Wi-Fi until the user unlocks it. Apple encrypts saved Wi-Fi credentials until unlock. Until then, Intune can't communicate with the device.
::: zone-end

::: zone pivot="windows"
When the 5‑minute restart timer starts, Windows attempts to show the notification: *Your device administrator has scheduled a reboot.* Delivering the restart command requires Windows Notification Services (WNS).

For more information about WNS, see [Network endpoint requirements](../../fundamentals/endpoints.md#windows-push-notification-services-wns-dependencies).
::: zone-end

## Reference links

::: zone pivot="windows"
- Configuration service provider (CSP) used to initiate the action: [Reboot CSP][CSP-1]
::: zone-end
- Microsoft Graph API: [rebootNow action][GRAPH-1]

<!--links-->

<!-- graph -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rebootnow

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- roles -->

[INT-R1]: ../../fundamentals/role-based-access-control/ref-built-in-roles.md#help-desk-operator
[INT-R2]: ../../fundamentals/role-based-access-control/ref-built-in-roles.md#school-administrator
[INT-R4]: ../../fundamentals/role-based-access-control/ref-built-in-roles.md#endpoint-security-manager
[INT-RC]: ../../fundamentals/role-based-access-control/create-custom-role.md

[IOS-SUP]: /intune/intune-service/remote-actions/device-supervised-mode

[CSP-1]: /windows/client-management/mdm/reboot-csp

::: zone pivot="windows,ios,macos,android,chromeos"
::: zone-end
