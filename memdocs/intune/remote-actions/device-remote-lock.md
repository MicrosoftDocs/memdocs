---
# required metadata

title: Lock devices with Microsoft Intune - Azure | Microsoft Docs
description: Use the Remote lock action in Microsoft Intune to lock a device that is protected by a PIN or password. 
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Remotely lock devices with Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The **Remote lock** device action locks the device. To unlock the device, the device owner enters their passcode. You can remotely lock devices that have a PIN or password set. Devices that don't have a PIN or password can't be remotely locked.

## Supported platforms

**Remote lock** is supported for the following platforms:

- Android
- Android enterprise kiosk devices
- Android enterprise work profile devices
- iOS
- macOS
- Windows 10 Mobile
- Windows Phone 8.1 and later

**Remote lock** isn't supported for:
- Windows 10 desktop

> [!NOTE]
> For macOS devices, you set a 6-digit recovery PIN. When the device is locked, the **Device overview** displays the PIN until another device action is sent. Please make sure to write down the pin since it will only be available for 30 days after the remote lock command is sent. After the 30 days, Intune will no longer have the PIN. Also, do not initiate this command again for the same device until the original pin is used to sucessfully unlock the device. You should send this command, write down the pin, and until you use it to get into the macOS device successfully, do not send this command to the same device again.  


## Remote lock a device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Devices** > **All devices**.
4. In the list of devices, select a device, and then select the **Remote lock** action.

## Next steps

- To see the status of this action, select **Microsoft Intune** > **Devices** > **Device actions**. 
- For more actions that can help you manage your devices, see [Available actions](device-management.md).
