---
# required metadata

title: Use iOS/iPadOS Lost Mode With Microsoft Intune
description: Learn how to use lost mode in Microsoft Intune to remotely lock and display a custom message on the screen of a lost or stolen iOS or iPadOS device. This article explains how to configure the lock screen message and phone number, and provides important details about the security and privacy implications of using lost mode.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management

---

# Use Lost Mode with Microsoft Intune

The **Lost Mode** device action in Microsoft Intune allows IT administrators to remotely lock and track lost or stolen iOS/iPadOS devices. When activated, lost mode displays a custom message and contact phone number on the device's lock screen—helping facilitate recovery while protecting corporate data.

Once enabled, the device is locked and cannot be accessed until lost mode is disabled by an administrator. While in lost mode, the device's location can also be tracked, making it easier to locate and recover.

Lost mode is a lightweight but powerful tool that helps organizations safeguard sensitive information, support device recovery, and maintain compliance—all without wiping or unenrolling the device.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - iOS in supervised mode
> - iPadOS in supervised mode

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] with the permissions:
>   - Remote tasks/Enable lost mode
>   - Remote tasks/Disable lost mode

## Enable lost mode

Here's how to enable lost mode on a device using the Intune admin center:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**](https://go.microsoft.com/fwlink/?linkid=2333814)
1. From the devices list, select a device, and then select **Lost mode (supervised only)**.
1. Under **Lost mode**, select **Enable**.
1. In the **Message to display on lock screen**, type a message to display on the device's lock screen.
1. Optionally, enter a phone number in the **Phone number to display** box.
1. Select **OK** to save your changes.

> [!TIP]
> In the message you enter to show on the lock screen, include specific details to return the lost device.

## User experience

When you enable lost mode, the device is locked, and the message you entered appears on the lock screen. The phone number you entered is also displayed on the lock screen. The user can't access the device until you disable lost mode.

While lost mode is enabled, use the [Locate device](device-locate.md) action to find the device.

> [!NOTE]
> Some built-in device functionalities might still work. For example, Siri might still be used to make calls unless it's disabled.

## Disable lost mode

Here's how to diable lost mode on a device using the Intune admin center:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**](https://go.microsoft.com/fwlink/?linkid=2333814)
1. From the devices list, select a device, and then **Lost mode (supervised only)**.
1. Under **Lost mode**, select **Disable**.
1. Select **OK** to save your changes.

## Security and privacy information for the lost mode and Locate device actions

- No device location information is sent to Intune until you turn on this action.
- When you use the **Locate** device action, the latitude and longitude coordinates of the device are sent to Intune, and shown in the Azure portal.
- The data is stored in Intune for 24 hours, then removed. You can't manually remove the location data.
- Location data is encrypted, both while stored, and while in transit.

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for these actions, see [enableLostMode action][GRAPH-1] and [disableLostMode action][GRAPH-2] in the Microsoft Graph API documentation.

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/intune-devices-manageddevice-enablelostmode
[GRAPH-2]: /graph/api/intune-devices-manageddevice-disablelostmode
