---
title: "Intune Remote Action: Rotate FileVault Recovery Key"
description: Learn how to rotate the FileVault recovery key with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Rotate FileVault recovery key

The **Rotate FileVault recovery key** remote action in Microsoft Intune allows IT admins to manually generate a new personal recovery key for a macOS device encrypted with FileVault. This action is useful when the current key is lost, potentially exposed, or needs to be refreshed for compliance or support reasons.

Once triggered, the new recovery key is securely stored in Intune and made available to the user through the Company Portal app or website. This action is only supported for corporate-owned macOS devices that are encrypted with FileVault via Intune policy.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - macOS (corporate-owned)

### :::image type="icon" source="../media/icons/headers/config.svg" border="false"::: Device configuration requirements

> [!div class="checklist"]
> To use this remote action, make sure devices meet the following requirements:
>
> - Are encrypted with FileVault using an Intune disk encryption policy.
> - Are marked as *corporate-owned* in Intune.
> - Have the FileVault personal recovery key escrowed to Intune.

For more information, see Use [FileVault disk encryption for macOS with Intune][LEARN-1].

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Rotate filevault key**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to rotate BitLocker keys from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Rotate FileVault recovery key**.
1. Select **Yes** to confirm the action.

## Reference links

- Microsoft Graph API: [rotateFileVaultKey action][GRAPH-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotateFileVaultKey

[LEARN-1]: /intune/intune-service/protect/encrypt-devices-filevault
