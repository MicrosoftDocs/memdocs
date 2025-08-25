---
# required metadata
title: Update cellular data plan for iOS/iPadOS devices with Microsoft Intune
description: Learn how to update the cellular data plan for iOS/iPadOS devices that support eSIM.
ms.date: 05/10/2025
ms.topic: how-to

ms.reviewer: rashok
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
appliesto:
  - ✅ iOS/iPadOS
---

# Update cellular data plan

The **Update cellular data plan** remote action lets you remotely activate eSIM cellular plan on iOS/iPadOS devices that support it.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - iOS
> - iPadOS

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] with the permission:
>   - RRemote tasks/Update cellular data plan

## Remotely update the cellular data plan

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From the devices list, select a device, and then select **...** > **Update cellular data plan (preview)**.
    ![Screenshot of updating cellular data plan](./media/images/update-cellular-data-plan.png)
1. Enter the activation server URL for your mobile carrier and select **Update cellular plan**.

## User experience

When you select the **Update cellular data plan** action, the device receives a command to activate the eSIM cellular data plan. The user experience on the device is as follows:

- Cellular data starts working.
- The active cellular data plan is listed in the cellular section of the **Settings** app on the device.

For more information about devices that support eSIM, see the Apple support article [Using Dual SIM with an eSIM](https://support.apple.com/HT209044).

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [activateDeviceEsim action][GRAPH-1].

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

[GRAPH-1]: /graph/api/intune-devices-manageddevice-activateDeviceEsim
