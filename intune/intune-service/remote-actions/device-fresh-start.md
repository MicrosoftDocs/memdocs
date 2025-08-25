---
# required metadata

title: Reset Windows 10 and 11 devices with Microsoft Intune
description: Use Fresh Start to remove or uninstall apps on Windows 10 and 11 by using Microsoft Intune.
ms.date: 04/07/2025
ms.topic: how-to

ms.reviewer:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Use Fresh Start to reset Windows 10 and 11 devices with Intune

The **Fresh Start** device action removes any apps that are installed on a PC running Windows 10, version 1709 or later and Windows 11. Fresh Start helps remove pre-installed (OEM) apps that are typically installed with a new PC.

<!--Initiate a Fresh start device action. This action removes any apps that are installed on a Windows 10 PC that is running the Creators Update. Then, it automatically updates the PC to the latest version of Windows.-->

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Windows 10/11

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - Endpoint Security Manager
> - [Custom role][INT-RC] with the permissions:
>   - Remote tasks/Clean PC


## How to execute Fresh Start

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices**, or use the following shortcut:
    > [!div class="nextstepaction"]
    > [All devices][INT-AC1]
1. From devices list, select a device, and then select **Fresh Start**.
1. Select **Retain user data on this device** to:
   -  Keep the device Microsoft Entra joined
   -  Device is enrolled into mobile device management again when a Microsoft Entra ID enabled user signs into the device.
   - Keep the contents of the device user's Home folder, and remove apps and settings

   > [!IMPORTANT]
   > If you do not retain user data, the device will be restored to the default OOBE (out-of-box experience) completed state retaining the built in administrator account.
   > BYOD devices will be unenrolled from Microsoft Entra ID and mobile device management.
   > Microsoft Entra joined devices will be enrolled into mobile device management again when a Microsoft Entra ID enabled user signs into the device.

1. Select **OK**.
1. The device will initiate the Fresh Start process.

## :::image type="icon" source="../media/icons/headers/microsoft-graph.svg" border="false"::: Microsoft Graph API reference

For more information about the API used for this action, see [cleanWindowsDevice action][GRAPH-1].

[GRAPH-1]: /graph/api/intune-devices-manageddevice-cleanwindowsdevice
