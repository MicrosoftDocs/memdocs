---
title: "Intune Remote Action: Deprovision"
description: Learn how to deprovision a chromeOS device with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---


# Deprovision chromeOS device

Select **Deprovision** to remove Google Admin policies from devices your organization no longer uses. To deprovision a ChromeOS device, you must be assigned a role that has the *Remote tasks: Retire* permission.

After you deprovision a device, it remains in the Intune admin center and the Google Admin console. Then on the admin center **System info** page, the device status changes to **DEPROVISIONED**. The device can't be enrolled again until you restore it to factory settings. For more information about the deprovision action, such as how to select the best reason for deprovisioning, see the [Chrome Enterprise and Education Help documentation](https://support.google.com/chrome/a/answer/3523633?).


## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - ChromeOS


> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>


## Reference links

- Microsoft Graph API: [ action][GRAPH-1]


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
