---
title: "Device Action: Fresh Start"
description: Learn how to use Fresh Start to remove or uninstall apps with Microsoft Intune.
ms.date: 10/27/2025
ms.topic: how-to
---

# Device action: Fresh Start

The *Fresh Start* action removes apps from managed Windows devices, helping you remove preinstalled (OEM) apps that typically ship with a new PC.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This action supports the following platforms:
>
> - Windows

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To run this action, use an account with at least one of the following roles:
>
> - [Help Desk Operator]
> - [School Administrator]
> - [Endpoint Security Manager]
> - [Custom role] that includes:
>   - The permission **Remote tasks/Clean PC**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::

## How to run Fresh Start from the Intune admin center

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of action icons. Select **Fresh Start**.
1. Select **Retain user data on this device** to:

   - Keep the device Microsoft Entra joined.
   - Automatically re-enroll the device in mobile device management when a Microsoft Entra ID-enabled user signs in.
   - Preserve the contents of the user's Home folder, while removing apps and settings.

   > [!IMPORTANT]
   > If you don't retain user data, the device is restored to the default out-of-box experience (OOBE) completed state retaining the built-in administrator account.
   > BYOD devices are removed from Microsoft Entra ID and mobile device management.

1. Select **OK**.

## Reference links

- Configuration service provider (CSP) used to initiate the action: [CleanPC CSP][CSP-1]
- Microsoft Graph API: [cleanWindowsDevice action][GRAPH-1]

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices

<!--Role links-->

[Help Desk Operator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#help-desk-operator
[School Administrator]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#school-administrator
[Endpoint Security Manager]: /intune/fundamentals/role-based-access-control/ref-built-in-roles#endpoint-security-manager
[Custom role]: /intune/fundamentals/role-based-access-control/create-custom-role

<!--Graph API links-->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-cleanwindowsdevice

<!--Other links-->

[CSP-1]: /windows/client-management/mdm/cleanpc-csp
