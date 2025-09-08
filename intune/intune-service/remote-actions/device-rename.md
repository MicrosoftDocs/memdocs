---
title: Rename a device with Microsoft Intune
description: Rename a device by using Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid:

ms.reviewer: Elcox
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Rename a device in Intune

You can use the **Rename device** action to change the **Device name** in the Microsoft Intune admin center for a device enrolled in Intune. The Rename action doesn't change the **Management name** in the Intune admin center or the **Device name** in the Company Portal.

For more information, on modifying the Management name and renaming in the Company Portal go to:

- [View device details with Microsoft Intune](../fundamentals/device-inventory.md#hardware-device-details).
- [Rename device from the Intune Company Portal app for Windows](../user-help/rename-your-device-cpapp.md).

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)
> - Android Enterprise corporate-owned Work Profile (COPE)
> - iOS/iPadOS in [Supervised Mode][IOS-SUP]
> - macOS
> - macOS (corporate-owned)
> - Windows (corporate-owned)

> [!NOTE]
> Renaming Android Enterprise devices only changes the **Device name** in the Intune admin center and not on the device itself. The Device name in Intune is a friendly name that users can change.

If a device isn't listed here, it isn't supported. This feature doesn't support renaming hybrid Microsoft Entra Windows devices.

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Set device name**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to rename a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **...** > **Rename device**.
1. In the **Rename device** pane, type the new name in the text box. You can use letters, numbers, and hyphens. The name must contain at least one letter or hyphen. Android Enterprise dedicated, fully managed, and corporate-owned work profile devices are an exception, and don't require a letter or hyphen.
1. If you want to restart the device after renaming it, Select **Yes** next to **Restart after rename**.
1. Select **Rename**.

> [!NOTE]
> If you have an iOS enrollment profile with a Device Name Template, the device will be renamed but will revert to the template after the next sync with Intune.

> [!NOTE]
> It could take 10 minutes or more for a renamed Android Enterprise device to update in the **Devices** area.

### Windows device rename rules

When you rename a Windows device, the new name must follow these rules:

- Less than or equal to 63 characters, not including trailing NULL
- Not null or an empty string
- Allowed ASCII: Letters (a-z, A-Z), numbers (0-9), and hyphens
- Allowed Unicode: characters >= 0x80, must be valid UTF8, must be IDN-mappable (that is, RtlIdnToNameprepUnicode succeeds; see RFC 3492)
- Names must not contain only numbers
- No spaces in the name
- Disallowed characters: `{ | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % `` ( ) + / , . _ *)`

## How to bulk rename devices

You can choose to rename devices in bulk, based on the device platform. The bulk rename option uses the same rules as renaming a single device. However, you must also include one of the following variables as part of the device name:

- **{{serialnumber}}** - Add the device's serial number to the name.
- **{{rand:x}}** - Add a random string of numbers, where x equals the number of digits to add.

To use the bulk rename action:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices** > **Bulk Device Actions**.
3. On the Basics page, for *OS* select the platform of the devices you want to rename, and then for *Device action* select **Rename**.
4. Complete the configuration wizard.

## Next steps

To see the status of the **Rename** device action, check the **Overview** page for the device.

## Reference links

- Microsoft Graph API: [setDeviceName action][GRAPH-1]


<!--links-->

<!-- graph -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-setdevicename

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[IOS-SUP]: /intune/intune-service/remote-actions/device-supervised-mode