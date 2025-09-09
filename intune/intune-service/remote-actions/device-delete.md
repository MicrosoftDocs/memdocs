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

zone_pivot_groups: 51e33912-415a-402f-8201-8acebf3e4991
---

# Delete devices using Intune

Use the **Delete** remote action in Intune to permanently remove devices that are no longer needed, being repurposed, or missing. This action helps clean up your device inventory and ensures that unmanaged or obsolete devices no longer appear in the admin center.

When using the **Delete** action, Intune issues a **Retire** or **Wipe** action depending on the platfrom and enrollment type. The following table details the expected behavior based on the device platform and the enrollment type.

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
| Windows | All                                        | RETIRE - All Profiles are deleted, work or school account is signed out  |
| macOS   | All                                        | RETIRE - All Profiles are deleted, CP app is deleted                      |

::: zone pivot="windows"

## Before you start

Before retiring a Microsoft Entra ID joined device, make sure to back up any critical data that may be lost during the process, such as:

- BitLocker recovery key
- Local administrator account credentials

::: zone-end

> [!IMPORTANT]
> The **Delete** action triggers the following actions:
>
> * Depending on the device platform, it can retire the Microsoft Entra device record / unjoin the device from Microsoft Entra ID. For more information, see [Retire](device-retire.md) section for the expected behavior.

<!-->
⚠️ Important Note on Deletion vs. Retire
If you delete the Intune object for a Microsoft Entra joined device that is protected by BitLocker, Intune triggers a sync that removes key protectors, which suspends BitLocker on the OS volume. This is a safeguard to prevent unrecoverable encryption scenarios when the Entra object is deleted.

✅ Best Practice
Before retiring or deleting a device:

Back up the BitLocker recovery key to a secure location (Microsoft account, Azure AD, USB, or file).
Ensure access to the Microsoft Entra ID object if recovery is needed later.
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