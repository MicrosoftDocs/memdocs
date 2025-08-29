---
# required metadata

title: "Intune Remote Device Action: Reset Passcode"
description: Learn how to reset a passcode with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
#SME:ileanawu
ms.collection:
- tier2
- M365-identity-device-management
---

# Reset a device passcode with Intune

With the **reset passcode** action in Microsoft Intune, you can remotely reset a device passcode to help users regain access to their devices without requiring a full device wipe. This remote action is especially useful when a user forgets their passcode or is locked out of their device or work profile.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
> - Android Enterprise personally-owned work profile (BYOD)
> - Android Open Source Project (AOSP)

## Passcode reset types

When working with Android devices, it's important to understand the two types of passcode resets available:

- **Device-level passcode reset**: The action resets the passcode for the entire device.
- **Work profile passcode reset**: The action resets the passcode for the user's work profile only.

The following table summarizes the passcode reset types based on platform:

| Platform | Device-level passcode reset | Work profile passcode reset |
|--|:-:|:-:|
| Android Enterprise corporate-owned dedicated (COSU) | ✅ | ❌ |
| Android Enterprise corporate-owned fully managed (COBO) | ❌ | ✅ |
| Android Enterprise corporate-owned work profile (COPE) | ❌ | ✅ |
| Android Enterprise personally-owned work profile (BYOD) | ❌ | ✅ |
| Android Open Source Project (AOSP) | ✅ | ❌ |

> [!IMPORTANT]
> Before initiating a passcode reset, ensure that the passcode requirement is enforced via [device configuration policies][INT-1]—otherwise, the reset fails.

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote Tasks/Reset Passcode**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Managed devices/Read, Update)

## How to reset a passcode

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **...** > **Reset passcode**.
1. A new passcode is presented to the admin.

The new passcode must be entered on the device, and it's displayed in the admin center for seven days.

## User experience

For work profile passcode reset, users get notified to activate their reset passcode. After their passcode is entered, the notification is dismissed.

>[!NOTE]
>If the remote lock action fails, confirm that you have a device passcode policy assigned to the device. If the device doesn't have a device passcode assigned, the remote lock action doesn't succeed.

## Reference links

- Microsoft Graph API: [resetPasscode action][GRAPH-1]

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-AC2]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/DeviceActionList.ReactView
[INT-1]:/intune/intune-service/configuration/settings-catalog-android

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/intune-devices-manageddevice-resetpasscode
