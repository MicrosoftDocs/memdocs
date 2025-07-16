---
# required metadata

title: View per-device software update reports for Apple devices in Microsoft Intune 
description: Use Microsoft Intune to view per-device software updates reports for managed Apple devices.
keywords:
author: brenduns
ms.author: brenduns
manager: laurawi
ms.date: 07/22/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- sub-updates
---

# Use the per-device declarative Apple software update reports in Microsoft Intune

Microsoft Intune’s declarative Apple software update reports for Apple devices relies on a reporting model that's part of Apple devices that provides near real-time status for Apple software updates. Available in Intune as a per-device report, these reports include the status information as reported directly by an Apple device each time the device’s software update status changes.

Applies to:

- iOS 17 and later
- iPadOS 17 and later
- macOS 13 and later

> [!NOTE]  
> With the availability of the declarative software update report for macOS, the previously available report for macOS devices named Software updates is now deprecated. This report remains available as *Software updates (deprecated)* when you go to *Devices* in the admin center and select a macOS device. While this report remains available for use in the Intune admin center, its being removed in a future update.

## About the reports
To find the per-device reports for iOS, iPadOS and macOS, sign-in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > select either *iOS/iPadOS* or *macOS*, and then select a device.

On the devices *Overview* page, expand *Monitor* and then depending on the type of device you're viewing select the report:

- For iOS and iPadOS, select **iOS software updates**.
- For macOS, select **macOS software updates**.

The following example is taken from the *macOS software updates* report:

:::image type="content" source="./media/software-update-report-apple-per-device/per-device-macos-software-updates.png" alt-text="Screen capture that shows the per-device report for a macOS device":::

In the per-device view, Intune displays the following information when successfully reported by the device:

- Current OS version 
- Current OS build 
- Latest available update for this device
- Pending OS version 
- Pending Build Version
- Install Reason
- Install State
- Last Reported Time - This value is the last time that the device synced with Intune.

You can also view Apple public update information in the report view when made available by Apple.

To learn more about the Apple declarative device management process, see [Installing and enforcing software updates for Apple devices](https://support.apple.com/guide/deployment/installing-and-enforcing-software-updates-depd30715cbb/web) in the Apple documentation.

## Related content

- [iOS/iPadOS update policies](../protect/software-updates-ios.md)
- [macOS update policies](../protect/software-updates-macos.md)