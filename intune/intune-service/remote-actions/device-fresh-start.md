---
# required metadata

title: "Intune Remote Device Action: Fresh Start"
description: Learn how to use Fresh Start to remove or uninstall apps with Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Fresh Start in Microsoft Intune

The **Fresh Start** device action removes apps from managed Windows devices, helping you remove preinstalled (OEM) apps that typically ship with a new PC.

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
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Clean PC**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Managed devices/Read, Update)

## How to execute Fresh Start

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device, and then select **Fresh Start**.
1. Select **Retain user data on this device** to:

   - Keep the device Microsoft Entra joined.
   - Automatically re-enroll the device in mobile device management when a Microsoft Entra ID-enabled user signs in.
   - Preserve the contents of the user's Home folder, while removing apps and settings.

   > [!IMPORTANT]
   > If you don't retain user data, the device is restored to the default out-of-box experience (OOBE) completed state retaining the built-in administrator account.
   > BYOD devices are removed from Microsoft Entra ID and mobile device management.

1. Select **OK**.

## Reference links

- Configuration service provider (CSP) used to initiate the remote action: [CleanPC CSP][CSP-1]
- Microsoft Graph API reference: [cleanWindowsDevice action][GRAPH-1]

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