---
# required metadata

title: Erase a macOS device
titleSuffix: Microsoft Intune
description: Learn how to erase all data, including the operating system, from a macOS device.
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
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9

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

# Erase all data from a macOS device

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

You can erase all data from a macOS device, including the operating system. The device will also be removed from Intune management. No warning will be given to the end user.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **All devices** > choose the device you want to erase.
2. Click **More** > **Erase** > provide a 6-digit number for the **Recovery Pin**. This is the pin that you must give to the user so that they can reinstall the operating system on their device. Be sure to make a note of this pin because it won't be visible after the erase action completes.
![Screenshot](./media/device-erase/providepin.png)
3. Click **OK** to erase the device.
