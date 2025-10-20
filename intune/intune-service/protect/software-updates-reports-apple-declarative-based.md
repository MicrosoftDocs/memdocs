---
title: View declarative device management-based software update reports for Apple devices in Microsoft Intune
description: Use Microsoft Intune to software updates reports for managed Apple devices based on Apples declarative device management capabilities.
author: paolomatarazzo
ms.author: paoloma
ms.date: 08/18/2025
ms.topic: conceptual
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
- sub-updates
---

# Declarative software update reports for Apple devices in Microsoft Intune

Microsoft Intune’s declarative Apple software update reports for Apple devices relies on a reporting model that's part of Apple devices that provides near real-time status for Apple software updates. Intune surfaces the update status from this reporting model through several reports that include the status information as reported directly by each Apple device, each time the device’s software update status changes.


Available reports include:

- [Per-device software update report](#per-device-software-update-report) - Per-device software update reports are available in the Intune Admin center by going to *Devices* and then selecting an applicable device. Each report view is focused on update status for only the selected device.

- [Apple software update failures](#apple-software-update-failures) - With this operational report, you can view details across your entire managed Apple device fleet. This includes iOS, iPadOS, and macOS devices. Details include why the update failed to install and the timestamp of the last failure.

- [Apple software update report](#apple-software-update-report) - This organizational report displays details about pending and current software update information across your entire managed Apple device fleet. Intune checks with Apple once per day to identify newly available updates.

- [*Apple software update summary report*](#apple-software-update-summary-report) - The Apple software update summary report displays a high-level view of how many of your managed Apple devices report each of the available update statuses. This view is divided into separate areas for macOS, iOS, and iPadOS with each area having a platform specific chart. Each area also identifies the most recently available update version and when it was made available by Apple. Intune checks with Apple once per day to identify newly available updates.

To learn more about the Apple declarative device management process, see [Installing and enforcing software updates for Apple devices](https://support.apple.com/guide/deployment/installing-and-enforcing-software-updates-depd30715cbb/web) in the Apple documentation.

Applies to:

- iOS 17 and later
- iPadOS 17 and later
- macOS 13 and later

> [!NOTE]
> With the availability of the declarative software update report for macOS, the previously available report for macOS devices named Software updates is now deprecated. This report remains available as *Software updates (deprecated)* when you go to *Devices* in the admin center and select a macOS device. While this report remains available for use in the Intune admin center, its being removed in a future update.

## Per-device software update report

Intune per-device reports  provide a software updates view that is focused on a single device. To find this view, sign-in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > select either *iOS/iPadOS* or *macOS*, and then select a device.

On the devices *Overview* page, expand *Monitor* and then depending on the type of device you're viewing select the report:

- For iOS and iPadOS, select **iOS software updates**.
- For macOS, select **macOS software updates**.

In the per-device view, Intune displays the following information about the devices update status as reported by the device:

- Current OS version
- Current OS build
- Latest available update for this device
- Pending OS version
- Pending Build Version
- Install Reason
- Install State
- Last Reported Time - This value is the last time that the device synced with Intune.

The following example is taken from the *macOS software updates* report:

:::image type="content" source="./media/software-updates-reports-apple-declarative-based/per-device-macos-software-updates.png" alt-text="Screen capture that shows the per-device report for a macOS device":::

## Apple software update failures

With the **Apple software update failures** operational report, you can view details for your managed iOS, iPadOS, and macOS device that are reporting update failures.

Details available in this report include:

- A list of devices that includes the device name, platform, current OS version, pending OS version, and more.
- Details include the failure reason and timestamp of last failure.
- An option to *Refresh* the report view.
- An option to *Export* the report details as a comma-separated values (.csv) file.

To find this report, in the admin center go to *Devices* > *Monitor*, and then select the report’s name to view the report details.

<!-- Image is pending availability
The following image is an example of the Apple update failures report for a test tenant:

:::image type="content" source="./media/software-updates-reports-apple-declarative-based/FILE.png" alt-text="Screen capture that shows the Apple software update failures report.":::
-->

## Apple software update report

As an organizational report, use the **Apple software update report** to view details about current software update status across your fleet of managed iOS, iPadOS, and macOS devices.

Details available in this report include:

-	When the report view was last generated (refreshed)
-	A chart view that identifies device counts for each software update status type
-	A list of devices with their most recent update status, which includes the device name, platform, current OS version, pending OS version, and more.

This report supports filters to focus results by platforms and update installation status. When you select the *Generate* button the report fetches relevant details for display based on the filters that are selected for platforms and update install states. The report also includes an option to *Export* the report details as a comma-separated values (.csv) file.

To find this report, in the admin center go to *Reports* > *Device management* > *Apple updates*, select the *Reports* tab, and then select the report tile.

The following image shows a blank report with no device details available, captured from a newly provisioned Intune tenant.

:::image type="content" source="./media/software-updates-reports-apple-declarative-based/apple-software-update-report.png" alt-text="Screen capture that shows the Apple software update report.":::

## Apple software update summary report

With the Apple software update **Summary** view, you monitor details about pending and current software update status across your fleet of managed iOS, iPadOS, and macOS devices.

This summary view presents the following for each device platform:

-	When the summary was last refreshed
-	The latest update that is available for the platform
-	When the latest update became available
-	A chart view that identifies device counts for each software update status category

To find this report, in the admin center go to *Reports* > *Device management* > *Apple updates*, select the *Summary* tab.

The following image shows a blank summary report with no device details available, captured from a newly provisioned Intune tenant:

:::image type="content" source="./media/software-updates-reports-apple-declarative-based/apple-update-summary-report.png " alt-text="Screen capture that shows the Apple software update Summary view.":::

## Related content

- [iOS/iPadOS update policies](../protect/software-updates-ios.md)
- [macOS update policies](../protect/software-updates-macos.md)

