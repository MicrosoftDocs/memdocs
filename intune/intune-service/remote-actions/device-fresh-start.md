---
title: "Remote Device Action: Fresh Start"
description: Learn how to use Fresh Start to remove or uninstall apps with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Remote device action: Fresh Start

The *Fresh Start* remote action removes apps from managed Windows devices, helping you remove preinstalled (OEM) apps that typically ship with a new PC.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
>
> - Windows

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Endpoint Security Manager][INT-R4]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Clean PC**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
## How to execute Fresh Start from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Fresh Start**.
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
- Microsoft Graph API: [cleanWindowsDevice action][GRAPH-1]

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