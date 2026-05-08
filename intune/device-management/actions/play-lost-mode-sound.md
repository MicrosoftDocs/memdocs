---
title: "Device Action: Play Lost Mode Sound"
description: Learn how to use the Play lost device sound action in Microsoft Intune to trigger an audible alert on a lost, stolen, or misplaced device—helping users locate it quickly and securely.
ms.date: 10/27/2025
ms.topic: how-to
zone_pivot_groups: 22f7442d-9384-49c8-abff-aaa058b30589
---

# Device action: play lost mode sound

Microsoft Intune provides platform-specific device actions to help locate a lost or misplaced device by triggering an audible alert—even if the device is locked or silenced.

- On iOS/iPadOS, use the *play Lost Mode sound* action. This action is available when the device is in [Lost Mode](lost-mode.md) and supervised.
- On Android Enterprise devices, use the *Play lost device sound* action. This action is supported for corporate-owned devices enrolled with Android Enterprise.

These device actions are especially useful in environments where devices are shared or frequently moved—such as classrooms, labs, or enterprise workspaces. Playing a sound helps users or administrators locate the device quickly and securely, supporting recovery efforts when a device is lost.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
> - iOS/iPadOS in [Supervised Mode](../../device-enrollment/apple/enable-supervised-mode.md)
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
::: zone pivot="ios"

> To use this action, make sure devices meet the following requirements:
>
> - Enable [Lost Mode](lost-mode.md)

::: zone-end

::: zone pivot="android"
> To use this action, make sure devices meet the following requirements:
>
> - Intune app is installed.

::: zone-end

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this action, use an account with at least one of the following roles:
>
> - [Help Desk Operator]
> - [School Administrator]
> - [Custom role] that includes:
>   - The permission **Remote tasks/Play sound to locate lost devices**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to play lost mode sound from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
::: zone pivot="ios"
3. At the top of the device overview pane, locate the row of action icons. Select **Play Lost Mode sound (supervised only)**.
::: zone-end
::: zone pivot="android"
3. At the top of the device overview pane, locate the row of action icons. Select **Play lost device sound**.
::: zone-end
4. Select the duration for the sound to play on the device, and then select **Yes**.

## User experience

::: zone pivot="ios"
The sound plays until the user disables the sound or the duration you set expires.
::: zone-end
::: zone pivot="android"

If system notifications are enabled, the device displays a notification with a **Stop Sound** button. The alert plays for the configured duration or until a user on the device manually stops it using the notification.

Notification behavior might vary based on system settings. To configure system notifications, see [Android Enterprise device settings to allow or restrict features using Intune](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

::: zone-end

## Reference links

- Microsoft Graph API: [playLostModeSound action][GRAPH-1]

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!--Role links-->

[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role
[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#help-desk-operator
[School Administrator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#school-administrator

<!--Graph API links-->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-playlostmodesound
