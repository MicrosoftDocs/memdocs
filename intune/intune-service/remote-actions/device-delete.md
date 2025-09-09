---
title: "Intune Remote Device Action: Delete"
description: Learn how to delete devices with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Delete devices using Intune

By using **Delete** actions, you can remove devices from Intune that are no longer needed, being repurposed, or missing.

<!--

If you want to remove devices from the Intune admin center, you can delete them from the specific device pane. Intune issues a **Retire** or **Wipe** action depending on the OS/Enrollment type. Not all enrollment types support the **Retire** action. See the following table for the expected behavior based on the device platform and the enrollment type.

| OS      | Enrollment Type                            | Action triggered                                                          |
|---------|--------------------------------------------|---------------------------------------------------------------------------|
| Android | Device administrator                       | RETIRE - All Profiles are deleted, Company Portal (CP) app is signed out. |
| Android | Personally owned devices with work profile | RETIRE - All Profiles are deleted, CP app is deleted.                     |
| Android | Corporate-owned devices with work profile  | WIPE                                                                      |
| Android | Dedicated devices                          | WIPE                                                                      |
| Android | Dedicated w/ Entra ID Shared Mode          | WIPE                                                                      |
| Android | Fully managed user devices                 | WIPE                                                                      |
| Android | AOSP Userless/AOSP User-Associated         | WIPE                                                                      |
| iOS     | All                                        | RETIRE - All Profiles are deleted, CP app is signed out                   |
| Windows | All                                        | RETIRE - All Profiles are deleted, work and school account is signed out  |
| macOS   | All                                        | RETIRE - All Profiles are deleted, CP app is deleted                      |

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices** > choose the devices you want to delete > **Delete**.

> [!IMPORTANT]
> The **Delete** action triggers the following actions:
>
> * Depending on the device platform, it can retire the Microsoft Entra device record / unjoin the device from Microsoft Entra ID. For more information, see [Retire](device-retire.md) section for the expected behavior.
> * BitLocker encryption is suspended if managed by Intune. To create a BitLocker profile, see [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md).

-->

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - All platforms

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Managed devices/Delete**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

## How to delete a device from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Delete**. To confirm, select **Yes**.

[!INCLUDE [multiple-administrative-approval](includes/multiple-administrative-approval.md)]

[!INCLUDE [remove-device-from-entra-id](includes/remove-device-from-entra-id.md)]

::: zone pivot="ios,macos"

[!INCLUDE [remove-apple-ade-device](includes/remove-apple-ade-device.md)]

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