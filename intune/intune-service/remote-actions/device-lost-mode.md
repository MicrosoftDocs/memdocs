---
title: "Remote Device Action: Lost Mode"
description: Learn how to enable Lost Mode in Microsoft Intune to remotely lock a lost or stolen iOS or iPadOS device and display a custom message and phone number on the lock screen.
ms.date: 09/22/2025
ms.topic: how-to
zone_pivot_groups: 46b8d067-28e2-43a6-97b2-ffcc8414e503
---

# Remote device action: Lost Mode

The *Lost Mode* device action in Microsoft Intune allows IT administrators to remotely lock and track lost or stolen devices. When activated, Lost Mode displays a custom message and contact phone number on the device's lock screen—helping facilitate recovery while protecting corporate data.

::: zone pivot="ios"
Once enabled, the device is locked and can't be accessed until Lost Mode is disabled by an administrator. While in Lost Mode, the device's location can also be tracked with the **[Locate device](device-locate.md)** action, making it easier to recover.
::: zone-end

::: zone pivot="chromeos"
Chrome Enterprise and the Google Admin console refer to devices in lost mode as *disabled*. For more information about how to disable a device, see the Chrome Enterprise and Education Help documentation.
::: zone-end

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - iOS/iPadOS in [Supervised Mode](/intune/intune-service/remote-actions/device-supervised-mode)
> - ChromeOS

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permissions **Remote tasks/Enable lost mode**, **Remote tasks/Disable lost mode**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to enable Lost Mode from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Lost mode (supervised only)**.
1. Under **Lost mode**, select **Enable**.
1. In the **Message to display on lock screen**, type a message to display on the device's lock screen.
1. Optionally, enter a phone number in the **Phone number to display** box.
1. Select **OK** to save your changes.

> [!TIP]
> In the message you enter to show on the lock screen, include specific details to return the lost device.

## User experience

When you enable Lost Mode, the device is locked. The custom message and phone number you specify are displayed on the lock screen, helping facilitate recovery. While Lost Mode is active, the user can't access the device.

::: zone pivot="ios"
To locate the device during this time, use the [Locate device](device-locate.md) action in the admin center.

> [!NOTE]
> Some built-in device functionalities might still work. For example, Siri might still be used to make calls unless it's disabled.

## How to disable Lost Mode from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then **Lost mode (supervised only)**.
1. Under **Lost mode**, select **Disable**.
1. Select **OK** to save your changes.

::: zone-end

## Reference links

- Microsoft Graph API:
  - [enableLostMode action][GRAPH-1]
  - [disableLostMode action][GRAPH-2]

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/intune-devices-manageddevice-enablelostmode
[GRAPH-2]: /graph/api/intune-devices-manageddevice-disablelostmode
