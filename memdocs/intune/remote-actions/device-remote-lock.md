---
# required metadata

title: Lock devices with Microsoft Intune
description: Use the Remote lock action in Microsoft Intune to lock a device that is protected by a PIN or password. 
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/17/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Remotely lock devices with Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The **Remote lock** device action locks the device. To unlock the device, the device owner enters their passcode. You can remotely lock devices that have a PIN or password set. Devices that don't have a PIN or password can't be remotely locked.

When **Remote lock** is applied to a device that doesn’t have a PIN or password, the device’s screen will turn off but the device will not be locked and the user will be able to wake the device and start using it again without entering a PIN or password. Ensure devices have a PIN or password policy enforced before using the **Remote lock** action to lock the device.

## Supported platforms

**Remote lock** is supported for the following platforms:

- Android
- Android Enterprise kiosk devices
- Android Enterprise work profile devices
- Android Enterprise fully managed devices
- Android Enterprise corporate-owned with work profile devices
- iOS
- macOS

**Remote lock** isn't supported for:
- Windows 10 desktop

> [!NOTE]
> For macOS devices, you set a 6-digit recovery PIN. When the device is locked, the **Device overview** displays the PIN until another device action is sent. Please make sure to write down the pin since it will only be available for 30 days after the remote lock command is sent. After the 30 days, Intune will no longer have the PIN. Also, you will see a failed status in reporting if you initiate this command again for the same device while the original pin has not been used to successfully unlock the device. You should only send this command once, write down the pin, and until you use it to get into the macOS device successfully, do not try to send this command to the same device again.


## Remote lock a device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Devices** > **All devices**.
4. In the list of devices, select a device, and then select the **Remote lock** action.

## Next steps

- To see the status of this action, select **Microsoft Intune** > **Devices** > **Device actions**. 
- For more actions that can help you manage your devices, see [Available actions](device-management.md).
