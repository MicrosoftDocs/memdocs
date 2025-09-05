---
title: Play Lost Mode Sound With Microsoft Intune
description: Learn how to use the play lost device sound action in Microsoft Intune to remotely trigger a sound alert on a lost or stolen device.
ms.date: 08/27/2025
ms.topic: how-to

ms.reviewer: shsivaku
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri

zone_pivot_groups: 22f7442d-9384-49c8-abff-aaa058b30589
---

# Play lost mode sound with Microsoft Intune

With Microsoft Intune, you can help users locate lost or misplaced devices by remotely triggering a sound alert.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> The **Play lost mode sound** action is supported on the following platforms:
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
> - iOS/iPadOS in [supervised mode](/intune/intune-service/remote-actions/device-supervised-mode) and [Lost Mode](device-lost-mode.md)

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Play sound to locate lost devices**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to play lost mode sound

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
::: zone pivot="ios"
2. From the devices list, select a device, and then select **...** > **Play Lost Mode sound (supervised only)**.
::: zone-end
::: zone pivot="android"
2. From the devices list, select a device, and then select **...** > **Play lost device sound**.
::: zone-end
3. Select the duration for the sound to play on the device, and then select **Yes**.

## User experience

::: zone pivot="ios"
The sound plays until the user disables the sound or the duration you set expires.
::: zone-end
::: zone pivot="android"

For **Android Enterprise dedicated devices**:

   - If notifications are enabled, a notification with a **Stop Sound** button shows up.
   - The sound plays for the set duration or, if notifications are enabled, until a user on the device turns it off.

To configure system notifications for devices in kiosk mode, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

For **Android Enterprise corporate-owned work profile devices**, and **Android Enterprise fully managed devices** :
   - To configure system notifications for devices, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

::: zone-end

## Reference links

- Microsoft Graph API: [playLostModeSound action][GRAPH-1]

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-AC2]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/DeviceActionList.ReactView

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/intune-devices-manageddevice-playlostmodesound
