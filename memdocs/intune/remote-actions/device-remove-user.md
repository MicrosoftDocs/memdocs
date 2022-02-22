---
# required metadata

title: Remove a user from an iOS/iPadOS device with Microsoft Intune 
titleSuffix:
description: Learn how to remove a user from a shared iOS/iPadOS device with Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7

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

# Remove a user from a shared iOS/iPadOS device


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The **Remove user** action deletes a user that you select from the local cache on a shared iPad device. The iPad device must be set up to manage the iOS/iPadOS Classroom app by using an [iOS/iPadOS education profile](../fundamentals/education-settings-configure-ios.md). 

## Supported platforms

- Windows - Not supported
- Windows Phone - Not supported
- iOS/iPadOS - Supported on iOS/iPadOS 9.3 and later (shared iPad devices only)
- macOS - Not supported
- Android - Not supported

## Remove a user

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. In the list of devices that you manage, select an iOS/iPadOS device.
4. In the pane for the device, select **Users**.
5. In the list, right-click the user that you want to remove, and then select **Remove user**.

## Next steps

- To see the status of the **Remove user** action, select **Devices** > **Device actions**.
