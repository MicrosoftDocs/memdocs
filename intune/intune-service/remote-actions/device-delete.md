---
title: "Remote Device Action: Delete"
description: Learn how to delete devices with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Remote device action: delete

Use the *delete* remote action in Intune to permanently remove devices that are no longer needed, being repurposed, or missing. This action helps cleanup your device inventory and ensures that unmanaged or obsolete devices no longer appear in the admin center.

### Delete remote action behavior by platform

When you use the **Delete** remote action in Intune, the command that triggers depends on the device platform and, for Android, the enrollment type.

- For **iOS/iPadOS**, **macOS**, and **Windows** devices, the Delete action always triggers a **Retire** command.
- For **Android** devices, the Delete action triggers either a **Retire** or **Wipe** command depending on the enrollment type.

| Platform   | Enrollment Type                      | Action Triggered           |
|------------|--------------------------------------|----------------------------|
| Windows    | Any                                  | [Retire](device-retire.md) |
| iOS/iPadOS | Any                                  | [Retire](device-retire.md) |
| macOS      | Any                                  | [Retire](device-retire.md) |
| Android    | Device administrator                 | [Retire](device-retire.md) |
| Android    | Personally-owned work profile (BYOD) | [Retire](device-retire.md) |
| Android    | Corporate-owned Fully managed (COBO) | [Wipe](device-wipe.md)     |
| Android    | Corporate-owned Dedicated (COSU)     | [Wipe](device-wipe.md)     |
| Android    | Corporate-owned Work profile (COPE)  | [Wipe](device-wipe.md)     |
| Android    | Open Source Project (AOSP)           | [Wipe](device-wipe.md)     |

::: zone pivot="windows"

## Before retiring or deleting a Microsoft Entra joined device

If you delete or retire the Intune object for a Microsoft Entra joined device that is protected by BitLocker, Intune triggers a sync that removes key protectors. This action suspends BitLocker on the OS volume as a safeguard to prevent unrecoverable encryption scenarios when the Entra object is deleted.

Before retiring a Microsoft Entra joined device, make sure to back up any critical data that might be lost during the process, such as:

- BitLocker recovery key
- Local administrator account credentials

::: zone-end

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
>
> - Android
> - iOS/iPadOS
> - macOS
> - Windows

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::

> To run this remote action, use an account with at least one of the following roles:
>
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Managed devices/Delete**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

:::column-end:::
:::row-end:::

## How to delete a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Delete**. To confirm, select **Yes**.

[!INCLUDE [multiple-administrative-approval](includes/multiple-administrative-approval.md)]

[!INCLUDE [remove-device-from-entra-id](includes/remove-device-from-entra-id.md)]

::: zone pivot="ios,macos"

[!INCLUDE [remove-device-from-apple-ade](includes/remove-device-from-apple-ade.md)]

::: zone-end

::: zone pivot="android"
::: zone-end

## Reference links

- Microsoft Graph API: [delete action][GRAPH-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-cleanwindowsdevice

[CSP-1]: /windows/client-management/mdm/cleanpc-csp