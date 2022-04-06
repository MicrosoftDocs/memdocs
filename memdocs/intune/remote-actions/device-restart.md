---
# required metadata

title: Restart devices with Microsoft Intune
description: Restart Windows and iOS/iPadOS devices using Microsoft Intune in the Azure portal using the Restart remote action.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5

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

# Remotely restart devices with Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The **Restart** device action causes the device you choose to be restarted (within 5 minutes). The device owner isn't automatically notified of the restart, and they might lose work.

## Supported platforms

- Windows - Supported on Windows 8.1 and later
    > [!Note] 
    > Windows attempts to show the user a message with the following text: "Your device administrator has scheduled a reboot." The message is shown when the 5 minute restart counter is started. Restart of Windows devices immediately requires push notifications via Windows Notification Services (WNS). 
    > For more information on WNS, see [Network Endpoint Requirements](/mem/intune/fundamentals/intune-endpoints#windows-push-notification-services-wns).
- Android Enterprise dedicated devices - Supported on Android 8.0 and later
- Android Enterprise fully managed devices - Supported on Android 8.0 and later
- Android Enterprise corporate-owned with work profile devices - Not supported 
- iOS/iPadOS - Supported

    > [!Note]  
    > This command requires a supervised device and the **Device Lock** access right. The device restarts immediately. Passcode-locked iOS/iPadOS devices don't rejoin a Wi-Fi network after restart. After restart, the device might not be able to communicate with the server.
- macOS - Not supported
- Android and Android Enterprise personally-owned work profile devices - Not supported

## Restart a device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Devices** > **All devices**.
4. In the list of devices that you manage, select a device > **Restart** > **Yes**.

## Next steps

- To see the status of the **Restart** device action, select **Devices** > **Device actions**.
