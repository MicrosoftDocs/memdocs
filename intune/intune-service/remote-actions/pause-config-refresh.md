---
# required metadata

title: Pause Config Refresh
description: Learn how Config Refresh can be paused for a configurable period of time, after which it's automatically re-enabled, or can be manually turned back on at any time by an IT administrator.
ms.date: 08/27/2025
ms.topic: how-to
#customerIntent: As an IT admin, I want to pause Config Refresh so that I can make changes or run remediation on a device for troubleshooting or maintenance.
ms.reviewer: Mike Danoski
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Pause Config Refresh in Intune

With Config Refresh, you can ensure that your settings are retained the way you configured them. Use the Windows [settings catalog](../configuration/settings-catalog.md) to set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune every 90 minutes by default, or every 30 minutes if desired.

To support this feature, there's a remote action that allows for a pause. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue the Pause action from Intune for a specified period. When the period expires, the settings are enforced again.

<!--It allows an Intune admin (or a custom role with this permission) to pause the periodic configuration refresh on a managed device.
This is typically used for troubleshooting scenarios where you don't want the device to reapply policies temporarily.
-->

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Windows 11

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Intune Administrator][ENT-R1]
> - [Custom role][INT-RC] with the permission:
>   - Remote tasks/Run Pause Configuration Refresh

## How to pause Config Refresh

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From the devices list, select a device.
1. Select **Pause Config Refresh**.
1. Specify the number of minutes to pause Config Refresh in the **Time period to Pause Config Refresh**. The maximum is 1,440 minutes (24 hours).
1. Select **Pause**.

> [!Note]
> If you pause a device that does not have Config Refresh enabled it has no effect.
> If Config Refresh is paused and you want to resume, then select Pause again for 0 minutes to resume Config Refresh enforcement.

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [pauseConfigurationRefresh action][GRAPH-1] in the Microsoft Graph API documentation.

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices
[ENT-R1]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[GRAPH-1]: /graph/api/intune-devices-manageddevice-pauseconfigurationrefresh

