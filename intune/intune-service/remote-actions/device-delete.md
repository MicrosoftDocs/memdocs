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

If [multi-admin approval access policies](../fundamentals/multi-admin-approval.md) are enabled for device actions, then some device actions might require a second administrator to approve. To learn more, see [Use Access policies to require multiple administrative approvals](../fundamentals/multi-admin-approval.md).

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>

## Delete devices from the Intune admin center

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

<a name='delete-devices-from-the-microsoft-entra-portal'></a>

## Delete devices from the Microsoft Entra admin center

You might need to delete devices from Microsoft Entra ID due to communication issues or missing devices. You can use the **Delete** action to remove device records from the Azure portal for devices that you know are unreachable and unlikely to communicate with Azure again. The **Delete** action doesn't remove a device from management.

1. Sign in to [Microsoft Entra ID in the Azure portal](https://azure.microsoft.com/services/active-directory/) by using your admin credentials. You can also sign in to the [Microsoft 365 admin center](https://admin.microsoft.com). From the menu, select **Admin centers** > **Microsoft Entra ID**.
1. Create an Azure subscription if you don't have one. The subscription shouldn't require a credit card or payment if you have a paid account (select the **Register your free Microsoft Entra ID** subscription link).
1. Select **Microsoft Entra ID**, and then select your organization.
1. Select the **Users** tab.
1. Select the user that's associated with the device that you want to delete.
1. Select **Devices**.
1. Remove devices as appropriate. For example, you might remove devices that are no longer in use, or devices that have inaccurate definitions.

::: zone-end

::: zone pivot="ios,macos"

[!INCLUDE [remove-apple-ade-device](includes/remove-apple-ade-device.md)]

::: zone-end

## Reference links

- Microsoft Graph API: [delete action][GRAPH-1]

