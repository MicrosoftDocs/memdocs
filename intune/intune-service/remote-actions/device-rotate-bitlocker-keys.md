---
# required metadata

title: "Intune Remote Device Action: BitLocker Key Rotation"
description: Learn how to rotate the BitLocker recovery keys with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# BitLocker key rotation with Intune

BitLocker key rotation is a security feature that allows IT administrators to remotely refresh the recovery keys used to unlock BitLocker-encrypted Windows devices. This process ensures that once a recovery key is used, or potentially exposed, it can be replaced with a new one, reducing the risk of unauthorized access.

BitLocker key rotation is important in environments where devices are frequently serviced, reassigned, or exposed to potential threats. For example, if a helpdesk technician provides a recovery key to a user during a support call, key rotation can be initiated from Intune, ensuring it can't be reused.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Windows

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] with the permission:
>   - Remote tasks/Rotate BitLockerKeys

## How to rotate BitLocker keys

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From the devices list, select a device, and then select **...** > **BitLocker key rotation**.
1. Select **Yes** to confirm the action.

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [rotateBitLockerKeys action][GRAPH-1].

## Related articles

To learn more about BitLocker, see [BitLocker overview][WIN-1].

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC1]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-rotateBitLockerKeys


<!-- MSLearn links -->

[WIN-1]: /windows/security/operating-system-security/data-protection/bitlocker/
