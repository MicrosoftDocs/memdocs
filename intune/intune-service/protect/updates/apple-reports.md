---
title: View Software Update Reports for Apple Devices
description: Track Apple device update status in real time with Intune's declarative software update reporting. Learn how Microsoft Intune surfaces update changes directly from managed Apple devices.
author: paolomatarazzo
ms.author: paoloma
ms.date: 10/14/2025
ms.topic: how-to
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
- sub-updates
---

# Software update reporting for Apple devices

Microsoft Intune uses Apple's declarative software update reporting model to provide near real-time status updates for managed Apple devices. This model enables Intune to surface update status directly from each device whenever its software update status changes.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> Software update reporting for Apple devices in Intune requires the following platforms:
>
> - iOS/iPadOS 17.0 and later
> - macOS 14.0 and later
:::column-end:::
:::row-end:::

## View software update reports

Intune provides several reports to help you monitor and troubleshoot software updates across your Apple device fleet:

- **Summary report**: Shows a high-level view of update status across macOS, iOS, and iPadOS devices, including the most recently available update version and release date.\
  Intune checks with Apple once per day to identify newly available updates.
- **Organizational report**: Displays pending and current update details across all managed Apple devices.
- **Failures report**: Lists update failures across macOS, iOS, and iPadOS devices, including failure reasons and timestamps.
- **Per-device report**: Focuses on the update status for an individual device.

Select a tab to learn more about each report. 

# [**Summary report**](#tab/summary)

With the Apple software update **Summary** view, you can monitor details about pending and current software update status across your fleet of managed iOS, iPadOS, and macOS devices.

This summary view presents the following information for each device platform:

- When you last refreshed the summary
- The latest update that's available for the platform
- When the latest update became available
- A chart view that identifies device counts for each software update status category

In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Device management** > **Apple updates** > **Summary**.

The following image shows a blank summary report with no device details available, captured from a newly provisioned Intune tenant:

:::image type="content" source="images/apple-update-summary-report.png " alt-text="Screen capture that shows the Apple software update Summary view.":::

# [**Organizational report**](#tab/organizational)

As an organizational report, use the **Apple software update report** to view details about the current software update status across your fleet of managed iOS, iPadOS, and macOS devices.

Details available in this report include:

- When the report view was last generated (refreshed)
- A chart view that identifies device counts for each software update status type
- A list of devices with their most recent update status, which includes the device name, platform, current OS version, pending OS version, and more

1. In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Device management** > **Apple updates** > **Reports**.
1. Select the tile **Apple software update report**.
1. Select the **Generate** button to populate the report view.

This report supports filters to focus results by platforms and update installation status. The report also includes an option to **Export** the report details as a comma-separated values (.csv) file.

The following image shows a blank report with no device details available, captured from a newly provisioned Intune tenant.

:::image type="content" source="images/apple-software-update-report.png" alt-text="Screen capture that shows the Apple software update report.":::

# [**Failures report**](#tab/failures)

With the **Apple software update failures** operational report, you can view details for your managed iOS, iPadOS, and macOS devices that report update failures.

Details available in this report include:

- A list of devices with their name, platform, current OS version, pending OS version, and more
- Details about the failure reason and timestamp of the last failure

In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Monitor** > **Apple software update failures**.

The reports include the option to **Refresh** the report view and to **Export** the report details as a comma-separated values (.csv) file.

# [**Per-device report**](#tab/per-device)

Intune per-device reports provide a software updates view that focuses on a single device.

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > select either **iOS/iPadOS** or **macOS**, then select a device.
1. On the device **Overview** page, expand **Monitor** and then, depending on the type of device you're viewing, select the report:
   - For iOS and iPadOS, select **iOS software updates**.
   - For macOS, select **macOS software updates**.

In the per-device view, Intune displays the following information about the device's update status as reported by the device:

- Current OS version
- Current OS build
- Latest available update for this device
- Pending OS version
- Pending Build Version
- Install Reason
- Install State
- Last Reported Time - This value is the last time that the device synced with Intune.

The following example is taken from the *macOS software updates* report:

:::image type="content" source="images/per-device-macos-software-updates.png" alt-text="Screen capture that shows the per-device report for a macOS device":::

---

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
