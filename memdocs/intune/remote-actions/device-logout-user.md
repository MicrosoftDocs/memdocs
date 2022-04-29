---
# required metadata

title: Log out the user of an iOS/iPadOS device 
titleSuffix: Microsoft Intune
description: Learn how to log out the current user of an iOS/iPadOS device with Intune."
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
ms.assetid: 702bc46c-1a6f-4689-bd53-3b778a447baa

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:  coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Logout the current user on Intune-managed iOS/iPadOS devices


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The **Logout current user** action logs out the current user on a shared iPad device. 

## Supported platforms

- Windows - Not supported
- Windows Phone - Not supported
- iOS/iPadOS - Supported on iOS/iPadOS 9.3 and later (shared iPad devices only)
- macOS - Not supported
- Android - Not supported

## How to log out the current user

1. Sign into the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices** > **All devices**.
2. Choose an iOS/iPadOS device > **...** > **Logout current user**.

## Next steps

To see the status of the action you just took, on the **Devices and groups** blade, choose **Device Actions**.
