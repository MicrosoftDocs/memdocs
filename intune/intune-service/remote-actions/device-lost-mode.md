---
title: "Intune Remote Actions: Lost Mode"
description: Learn how to enable Lost Mode in Microsoft Intune to remotely lock a lost or stolen iOS or iPadOS device and display a custom message and phone number on the lock screen.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management

---

# Use Lost Mode with Microsoft Intune

The **Lost Mode** device action in Microsoft Intune allows IT administrators to remotely lock and track lost or stolen iOS/iPadOS devices. When activated, Lost Mode displays a custom message and contact phone number on the device's lock screen—helping facilitate recovery while protecting corporate data.

Once enabled, the device is locked and can't be accessed until Lost Mode is disabled by an administrator. While in Lost Mode, the device's location can also be tracked, making it easier to locate and recover.

Lost Mode is a lightweight but powerful tool that helps organizations safeguard sensitive information, support device recovery, and maintain compliance—all without wiping or unenrolling the device.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - iOS/iPadOS in [Supervised Mode](/intune/intune-service/remote-actions/device-supervised-mode)

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permissions **Remote tasks/Enable lost mode**, **Remote tasks/Disable lost mode**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## Enable Lost Mode

Here's how to enable Lost Mode on a device using the Intune admin center:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **Lost mode (supervised only)**.
1. Under **Lost mode**, select **Enable**.
1. In the **Message to display on lock screen**, type a message to display on the device's lock screen.
1. Optionally, enter a phone number in the **Phone number to display** box.
1. Select **OK** to save your changes.

> [!TIP]
> In the message you enter to show on the lock screen, include specific details to return the lost device.

## User experience

When you enable Lost Mode, the device is locked. The custom message and phone number you specify are displayed on the lock screen, helping facilitate recovery. While Lost Mode is active, the user can't access the device.

To locate the device during this time, use the [Locate device](device-locate.md) action in the admin center.

> [!NOTE]
> Some built-in device functionalities might still work. For example, Siri might still be used to make calls unless it's disabled.

## Disable Lost Mode

Here's how to disable Lost Mode on a device using the Intune admin center:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then **Lost mode (supervised only)**.
1. Under **Lost mode**, select **Disable**.
1. Select **OK** to save your changes.

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
