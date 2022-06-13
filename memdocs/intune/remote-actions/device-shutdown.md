---
# required metadata

title: Shut down devices with Microsoft Intune
description: Shut down iOS/iPadOS devices using remote actions in Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 06/10/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5

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

# Remotely shut down devices using Intune

With the **Shut down** device action you can remotely power off devices. When you remotely shut down the device, no warning will be given to the end user.

## Supported platforms

 - iOS/iPadOS 10.3 and later
 - macOS 10.13 and later

> [!NOTE]
> This command requires a supervised device and the device shuts down immediately. iOS/iPadOS devices that are Passcode-locked will not rejoin a Wi-Fi network after restarting. After restarting, the device might not be able to communicate with the server.

## Shut down an iOS/iPadOS device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. In the list of devices that you manage, select a device > **Shut down (supervised only)** > **Yes**.

## Shut down a macOS device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. In the list of devices that you manage, select a device > **Shut down** > **Yes**.