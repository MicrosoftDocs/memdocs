---
# required metadata

title: Sync devices with Microsoft Intune - Azure | Microsoft Docs
description: Synchronize devices that are registered or managed with Microsoft Intune to get the latest policies and actions. Includes the steps to sync by using the Azure portal, and lists the error codes that can be retried.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/31/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 02ad249e-f098-421f-861f-6b2ff733ac7c

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

# Sync devices to get the latest policies and actions with Intune


The **Sync** device action forces the selected device to immediately check in with Intune. When a device checks in, it immediately receives any pending actions or policies that have been assigned to it. This feature can help you immediately validate and troubleshoot policies you've assigned, without waiting for the next scheduled check-in.

## Supported platforms

- Windows
- iOS
- macOS
- Android (Device administrator and Android for Work only)

## Sync a device

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 
3. Select **Devices** > **All devices**.
4. In the list of devices you manage, select a device to open its *Overview* pane, and then select **Sync**.
5. To confirm, select **Yes**.

To see the status of the sync action, choose **Devices** > **Monitor** > **Device actions**.

You can find standard Intune policy check-in frequencies in the [Refresh cycle times](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## Retryable error codes

When an administrator runs the **Sync** device action, iOS/iPadOS and Android apps that failed and raised a retryable error code are still available to the device. However, apps that raised a nonretryable error code must wait seven days before they're available to the device.


| Error code  | Suggested description | Retryable |
|---|---|---|
| 2016330898 | An unknown error occurred. | No |
| 2016330897 | Your connection to Intune timed out. Reset your connection. | Yes |
| 2016330896 | You lost connection to the Internet. Reset your connection. | Yes |
| 2016330895 | You lost connection to the Internet. Reset your connection. | Yes |
| 2016330894 | You lost connection to the Internet. Reset your connection. | Yes |
| 2016330893 | You lost connection to the Internet. Reset your connection. | Yes|
| 2016330892 | International roaming is disabled. | No|
| 2016330891 | The cellular data connection for this device can't be accessed while a phone call is being made. Wait for the phone call to complete. | Yes|
| 2016330890 | The cellular network for this device. These devices couldn't be used at this time. | No|
| 2016330889 | The secure connection failed. Reset your connection. | Yes|
| 2016330888 | The server trust evaluation has failed. | No|

## Next steps

You can [check the details](device-inventory.md) of the device.
 
