---
title: "Remote Device Action: Shutdown"
description: Learn how to shutdown Apple devices with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
---

# Remote device action: shut down

With the *shut down* action, IT administrators can remotely power off managed devices. This action doesn't prompt or warn the user before the device powers down.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - iOS/iPadOS in [Supervised Mode][IOS-SUP]
> - macOS

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Shut down**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to shut down a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Shut down** > **Yes**.

> [!NOTE]
> iOS/iPadOS devices that are Passcode-locked will not rejoin a Wi-Fi network after restarting. After restarting, the device might not be able to communicate with the server.

## Reference links

- Microsoft Graph API: [shutDown action][GRAPH-1]

<!-- links -->

[ENT-R1]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager

[IOS-SUP]: /intune/intune-service/remote-actions/device-supervised-mode

[GRAPH-1]: /graph/api/intune-devices-manageddevice-shutdown

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
