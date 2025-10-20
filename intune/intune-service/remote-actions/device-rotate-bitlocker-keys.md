---
title: "Remote Device Action: BitLocker Key Rotation"
description: Learn how to rotate the BitLocker recovery key with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
---

# Remote device action: BitLocker key rotation

The *BitLocker key rotation* remote action in Microsoft Intune lets IT admins remotely refresh the recovery key for the operating system drive on BitLocker-encrypted Windows devices. This helps reduce the risk of unauthorized access if a recovery key has been used or potentially exposed.

Key rotation is especially useful in environments where devices are frequently serviced, reassigned, or exposed to support scenarios. For example, if a helpdesk technician shares a recovery key during a support call, you can rotate the key from Intune to ensure it can't be reused.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - Windows

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Rotate BitLockerKeys**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to rotate the BitLocker key from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **BitLocker key rotation**.
1. Select **Yes** to confirm the action.

## Reference links

- Configuration service provider (CSP) used to initiate the remote action: [BitLocker CSP][CSP-1]
- Microsoft Graph API: [rotateBitLockerKeys action][GRAPH-1]
- [BitLocker overview][WIN-1]

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotateBitLockerKeys


<!-- MSLearn links -->

[WIN-1]: /windows/security/operating-system-security/data-protection/bitlocker/
[CSP-1]: /windows/client-management/mdm/bitlocker-csp#rotaterecoverypasswords
