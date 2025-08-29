---
# required metadata

title: Shut down devices with Microsoft Intune
description: Shut down iOS/iPadOS devices using remote actions in Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Remotely shut down devices using Intune

With the **shut down** action, IT administrators can remotely power off managed devices. This action doesn't prompt or warn the user before the device powers down

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - iOS/iPadOS in [supervised mode][IOS-SUP]
> - macOS

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Shut down**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Managed devices/Read, Update)

## How to shut down a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **...** > **Shut down** > **Yes**.

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
