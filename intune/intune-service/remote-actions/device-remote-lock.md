---
# required metadata

title: "Intune Remote Device Action: Remote Lock"
description: Use the remote lock action in Microsoft Intune to lock a managed device that has a passcode or PIN.
ms.date: 08/26/2025
ms.topic: how-to

ms.reviewer:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management

zone_pivot_groups: bf632d5b-6209-46d2-8c9c-8d76b1f704cc
---

# Remotely lock devices with Intune

The **Remote lock** device action locks a managed device so the user must enter the existing passcode or PIN to regain access. Use this action when a device is misplaced, left unattended, or suspected of unauthorized use, without wiping data or removing enrollment.

> [!IMPORTANT]
> Remote lock is only effective when the device already has a passcode or PIN. If no passcode exists, the screen may simply turn off and the user can still access the device. Enforce a passcode policy before relying on this action for protection.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Android
>     - Android Enterprise corporate owned dedicated (COSU)
>     - Android Enterprise corporate owned fully managed (COBO)
>     - Android Enterprise corporate owned work profile (COPE)
>     - Android Open Source Project (AOSP)
> - iOS/iPadOS
> - macOS

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - Endpoint Security Manager
> - [Custom role][INT-RC] with the permission:
>   - Remote tasks/Remote lock

## Remote lock a device

Here's how to remotely lock a device using the Intune admin center:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From the devices list, select a device, and then select **Remote lock**.
::: zone pivot="macos"
4. Set a six-digit recovery PIN.

>[!NOTE]
>When the device is locked, the **Device overview** displays the PIN until another device action is sent. Make sure to write down the pin since it will only be available for 30 days after the remote lock command is sent. After the 30 days, Intune will no longer have the PIN. Also, you get a *failed* status in reporting if you initiate this command again for the same device while the original pin hasn't been used to successfully unlock the device. You should only send this command once, write down the pin, and until you use it to get into the macOS device successfully, don't try to send this command to the same device again.

::: zone-end

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [remoteLock action][GRAPH-1].

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-remotelock
