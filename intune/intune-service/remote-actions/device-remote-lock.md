---
# required metadata

title: "Intune Remote Device Action: Remote Lock"
description: Use the remote lock action in Microsoft Intune to lock a managed device that has a passcode or PIN.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management

zone_pivot_groups: bf632d5b-6209-46d2-8c9c-8d76b1f704cc
---

# Remotely lock devices with Intune

The **Remote lock** device action locks a managed device so the user must enter the existing passcode or PIN to continue. Use this action when a device is misplaced, left unattended, or suspected of unauthorized use without wiping data or removing enrollment.

> [!IMPORTANT]
> Remote lock is only effective if a passcode or PIN is already set:
> - If no passcode exists, the screen may just turn off and the user can still access the device.
> - Enforce a passcode policy before relying on this action.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Android
>     - Android Enterprise corporate-owned dedicated (COSU)
>     - Android Enterprise corporate-owned fully managed (COBO)
>     - Android Enterprise corporate-owned work profile (COPE)
>     - Android Open Source Project (AOSP)
> - iOS/iPadOS
> - macOS

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission: **Remote tasks/Remote lock**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Read device, Update devices)

## How to remote lock a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**](https://go.microsoft.com/fwlink/?linkid=2333814)
1. From the devices list, select a device, and then select **Remote lock**.
::: zone pivot="macos"
3. Set a six-digit recovery PIN.

> [!NOTE]
> The recovery PIN is shown on the device overview pane for up to 30 days, or until another device action is sent. Record it securely; it can't be retrieved afterward. Don't resend remote lock to the same macOS device until that PIN is used—additional attempts show a **Failed** status in reporting.

::: zone-end

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [remoteLock action][GRAPH-1].

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-remotelock
