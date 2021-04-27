---
# required metadata

title: Find lost devices with Microsoft Intune - Azure | Microsoft Docs
description: Locate lost or stolen devices by using the locate device feature in Microsoft Intune. Get details on security and privacy information when using the locate device action.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 3e544286-12ad-4a3a-86f8-d2cf16940b1f

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

# Locate lost or stolen iOS/iPadOS or Windows devices with Intune

To get the location of a lost or stolen Windows or iOS/iPadOS device on a map, use the **Locate device** action.

## Supported platforms

- iOS/iPadOS 9.3 and later (These devices must be in supervised mode. Before you use this action, be sure the device is in [lost mode](device-lost-mode.md).)
- Windows 10 version 20H2 (10.0.19042.789) or later
- Windows 10 version 2004 (10.0.19041.789) or later
- Windows 10 version 1909 (10.0.18363.1350) or later
- Windows 10 version 1809 (10.0.17763.1728) or later

This feature isn't supported for the following systems:

- Windows Phone
- macOS
- Android

## Locate a lost or stolen device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices**, and then select **All devices**.
3. From the list of devices you manage, choose a Windows or iOS/iPadOS device, and choose **...**. Then choose the **Locate device** remote action.
4. After the device is located, its location is shown in **Locate device**.
    ![Screenshot of Locate device using Intune in Azure](./media/device-locate/locate-device.png)

## Activate lost mode sound alert on an iOS device

If someone has lost their iOS/iPadOS 9.3 or later device, you can remotely trigger the device to play an alert sound so the user can find it. The device must be in [lost mode](device-lost-mode.md).

In the [Intune in the Azure portal](https://aka.ms/intuneportal), choose **Devices** > **All devices** > select an iOS/iPadOS device > **Overview** > **More** > **Play Lost mode sound (supervise only)**.

The sound plays until the user disables the sound on the device or the device is removed from lost mode.

## Security and privacy information for lost mode and locate device actions

- No device location information is sent to Intune until you turn on this action.
- When you use the locate device action, the latitude and longitude coordinates of the device can be retrieved by using the Graph API.
- The data is stored for 24 hours, then removed. You can't manually remove the location data.
- Location data is encrypted, both while stored and while being transmitted.
- For iOS/iPadOS devices, when you configure lost mode, you can customize a message that appears on the lock screen. In this message, to help the person that finds the device, be sure to include specific details to return the lost device.

## Next steps

To see the status of enabling locate device, open **Devices**, and select **Device actions**.
