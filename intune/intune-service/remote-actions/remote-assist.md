---
title: "Intune Remote Device Action: New Remote Assistance Session"
description: Learn how to use the the new remote assistance session action in Intune to offer support to your users.
ms.date: 08/27/2025
ms.topic: how-to
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# New Remote Assistance Session

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platform:
>
> -
> -
> -
> -

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permissions `Microsoft.Intune_RemoteAssistance_Read`
>   - `Microsoft.Intune_RemoteAssistanceApp_Elevation`
>   - `Microsoft.Intune_RemoteAssistanceApp_TakeFullControl`
>   - `Microsoft.Intune_RemoteAssistanceApp_Unattended`
>   - `Microsoft.Intune_RemoteAssistanceApp_ViewScreen`
>   - `Microsoft.Intune_RemoteTasks_RequestRemoteAssistance`
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to offer remote assistance

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **...** > **New Remote Assistance Session**

## Reference links

- Microsoft Graph API: [action][GRAPH-1]




[Use Remote Help with Intune](../fundamentals/remote-help.md)
[See device details in Intune](../fundamentals/device-inventory.md)

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

<!-- API links -->

[GRAPH-1]: /graph/api/


<!-- MSLearn links -->

[WIN-1]: /windows/security/operating-system-security/data-protection/bitlocker/