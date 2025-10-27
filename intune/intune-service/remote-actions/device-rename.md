---
title: "Remote Device Action: Rename Device"
description: Learn how to use the Rename device remote action in Microsoft Intune to update the device name shown in the admin center. Useful for standardizing naming conventions, managing shared devices, and improving inventory clarity.
ms.date: 10/27/2025
ms.topic: how-to
zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Remote device action: rename

The *rename device* remote action in Microsoft Intune allows IT administrators to change the *Device name* displayed in the Intune admin center for a managed device. This action does not affect the *Management name* in Intune or the *Device name* shown in the Company Portal.

Renaming a device can help improve clarity and consistency across your device inventory—especially in environments with shared devices, standardized naming conventions, or large-scale deployments. It's useful for aligning device names with asset tags, user roles, or location-based identifiers, making it easier to manage and troubleshoot devices at scale.

::: zone pivot="android"

> [!NOTE]
> Renaming Android Enterprise devices only changes the **Device name** in the Intune admin center and not on the device itself. The Device name in Intune is a friendly name that users can change.

::: zone-end

::: zone pivot="windows"

> [!NOTE]
> Renaming Microsoft Entra hybrid joined devices from Intune is not supported. To rename hybrid joined devices, use domain-based methods outside of Intune.

::: zone-end

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)
> - Android Enterprise corporate-owned Work Profile (COPE)
> - iOS/iPadOS in [Supervised Mode][IOS-SUP]
> - macOS (corporate-owned)
> - Windows (corporate-owned)

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Set device name**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to rename a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Rename device**.
::: zone pivot="windows"
4. In the **Rename device** pane, type the new name in the text box. The new name must follow these rules:
    - Less than or equal to 63 characters, not including trailing NULL
    - Not null or an empty string
    - Allowed ASCII: Letters (a-z, A-Z), numbers (0-9), and hyphens
    - Allowed Unicode: characters >= 0x80, must be valid UTF8, must be IDN-mappable (that is, RtlIdnToNameprepUnicode succeeds; see RFC 3492)
    - Names must not contain only numbers
    - No spaces in the name
    - Disallowed characters: `{ | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % `` ( ) + / , . _ *)`
::: zone-end
::: zone pivot="ios,macos"
4. In the **Rename device** pane, type the new name in the text box. You can use letters, numbers, and hyphens. The name must contain at least one letter or hyphen.
::: zone-end
::: zone pivot="android"
4. In the **Rename device** pane, type the new name in the text box. You can use letters, numbers, and hyphens.
::: zone-end
5. If you want to restart the device after renaming it, Select **Yes** next to **Restart after rename**.
6. Select **Rename**.

::: zone pivot="ios"
> [!NOTE]
> If you have an iOS enrollment profile with a Device Name Template, the device will be renamed but will revert to the template after the next sync with Intune.
::: zone-end

::: zone pivot="android"
> [!NOTE]
> It could take 10 minutes or more for a renamed Android Enterprise device to update in the **Devices** list.
::: zone-end

## How to bulk rename devices from the Intune admin center

You can choose to rename devices in bulk, based on the device platform. The bulk rename option uses the same rules as renaming a single device. However, you must also include one of the following variables as part of the device name:

- `{{serialnumber}}` - Add the device's serial number to the name.
- `{{rand:x}}` - Add a random string of numbers, where x equals the number of digits to add.

To use the bulk rename action:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. Select **Bulk Device Actions**.
1. On the Basics page, for **OS** select the platform of the devices you want to rename, and then for **Device action** select **Rename**.
1. Complete the configuration wizard.

## Reference links

- Microsoft Graph API: [setDeviceName action][GRAPH-1]
::: zone pivot="windows"
- Configuration service provider (CSP) used to initiate the remote action: [Accounts CSP][CSP-1]
::: zone-end

## Next steps

To learn how to change the Device name shown in the Company Portal, see [Rename device from the Company Portal](../user-help/rename-your-device-cpapp.md).

<!--links-->

<!-- graph -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-setdevicename

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[IOS-SUP]: /intune/intune-service/remote-actions/device-supervised-mode

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[CSP-1]: /windows/client-management/mdm/accounts-csp
