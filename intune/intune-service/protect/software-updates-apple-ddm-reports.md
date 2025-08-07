---
title: Per-device Apple software update reports in Microsoft Intune
description: Reports for Apples declarative device management software updates in Microsoft Intune. View per-device status from each step of the software update process.
author: brenduns
ms.author: brenduns
manager: laurawi
ms.date: 08/18/2025
audience: ITPro
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:

ms.reviewer: beflamm
ms.suite: ems
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- sub-updates
---

# Per-device declarative Apple software update reports

Microsoft Intune’s declarative Apple software update reports for Apple devices relies on Apple's declarative device management (DDM) a reporting model that is built in to Apple devices. With DDM, devices proactively report rich, near real-time software update information each time the device’s software update status changes from downloading an update to its final installation.

Applies to:

- iOS 17 and later
- iPadOS 17 and later
- macOS 13 and later

> [!NOTE]
>
> With the availability of the declarative software update report for macOS, the previously available Software updates report for macOS devices is deprecated. The macOS software Updates (Deprecated) report remains available for use in the Intune admin center, but will be removed as part of a future update.

## About the reports

To find the per-device reports for iOS, iPadOS and macOS, sign-in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > select either *iOS/iPadOS* or *macOS*, and then select a device.

On the devices *Overview* page, expand *Monitor* and then depending on the type of device you're viewing select the report:

- For iOS an iPadOS, select **iOS software updates**
- For macOS, select **macOS software updates**

The following example is taken from the *macOS software updates* report:

:::image type="content" source="./media/software-updates-apple-ddm-reports/per-device-macos-software-updates.png" alt-text="Screen capture that shows the per-device report for a macOS device":::


In the per-device view, Intune displays the following information when successfully reported by the device:

- Current OS version 
- Current OS build 
- Latest available update for this device
- Pending OS version 
- Pending Build Version
- Install Reason
- Install State
- Last Reported Time

You can also find Apple public update information in the report view when made available by Apple. 

To learn more about the Apple declarative device management process, see [Installing and enforcing software updates for Apple devices](https://support.apple.com/guide/deployment/installing-and-enforcing-software-updates-depd30715cbb/web) in the Apple documentation.

## Related content

- [Managed software updates (DDM)](../protect/managed-software-updates-ios-macos.md)


