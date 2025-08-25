---
# required metadata

title: Restart devices with Microsoft Intune
description: Restart Windows and iOS/iPadOS devices using Microsoft Intune in the Azure portal using the Restart remote action.
ms.date: 10/27/2023
ms.topic: how-to

ms.reviewer:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Remotely restart devices with Intune

The **Restart** device action causes the device you choose to be restarted (within 5 minutes). The device owner isn't automatically notified of the restart, and they might lose work.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Android
>     - Corporate owned Fully Managed (COBO)
>     - Corporate-owned Dedicated (COSU)
>     - Android Open Source Project (AOSP)
> - iOS/iPadOS in [supervised mode][IOS-SUP]
> - macOS
> - Windows 10/11
> - ChromeOS

    > [!Note]
    > Windows attempts to show the user a message with the following text: "Your device administrator has scheduled a reboot." The message is shown when the 5 minute restart counter is started. Restart of Windows devices immediately requires push notifications via Windows Notification Services (WNS).
    > For more information on WNS, see [Network Endpoint Requirements](../fundamentals/intune-endpoints.md#windows-push-notification-services-wns-dependencies).

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - Endpoint Security Manager
> - [Custom role][INT-RC] with the permissions:
>   - Remote tasks/Reboot now

## How to restart a device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From devices list, select a device, and then select **Restart** > **Yes**.

## User experience

::: zone pivot="ios"

>[!NOTE]
>A passcode-locked iOS/iPadOS device doesn't automatically reconnect to Wi-Fi after a restart. This behavior is part of Apple's security model, which encrypts sensitive data—including saved Wi-Fi credentials—until the user unlocks the device. This behavior interrupts communication with Microsoft Intune until the device is unlocked.

:::endzone

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [rebootNow action][GRAPH-1].

<!--links-->

<!-- graph -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rebootnow

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!-- roles -->

[ENT-R1]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

[IOS-SUP]: /intune/intune-service/remote-actions/device-supervised-mode