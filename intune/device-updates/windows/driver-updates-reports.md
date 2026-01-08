---
title: Use Windows Update for Business reports for Windows Updates in Microsoft Intune
description: Use Windows Update for Business reports to view data for Windows Updates you deploy with Intune.
ms.date: 03/04/2025
ms.topic: how-to
ms.reviewer: zadvor
---

# Reports for Windows Driver updates policy

Intune offers integrated reports to view detailed status for Windows driver updates for devices assigned to Windows Driver update policies. To use these reports, you must first configure the prerequisites and policies that support data collection from devices. These reports are applicable to Windows 10 and Windows 11.

The data in the Intune reports for Windows Driver update policies is used only for these reports and doesn't appear in other Intune reports. The following reports are available:

- [Windows Driver updates summary](#windows-driver-updates-summary)
- [Windows Driver updates report](#windows-driver-updates-report)
- [Windows Driver update failures](#windows-driver-update-failures)

## Before you begin

> [!div class="checklist"]
> - Ensure your environment meets the requirements in [Windows driver updates overview](driver-updates.md#prerequisites).

### User permissions to use reports

To view these reports, users must be assigned an Intune role with the **Managed devices** > **View reports** permission. This permission is included in the following built-in roles:

- Endpoint Security Manager
- Read Only Operator
- Help Desk Operator

## Windows Driver updates summary

On the Summary tab of the Windows Updates node of Reports, you can view summary details about device success or failure for installing updates from device update policies. To find this report, navigate to **Reports** > **Windows Updates** > **Summary** tab and scroll down until you find the **Windows Driver updates**.

The following screen capture displays a summary of four policies, each assigned to a single device.

:::image type="content" source="./images/reports/report-driver-updates-summary.png" alt-text="Screen capture of the Windows Driver Updates summary page." lightbox="./images/reports/report-driver-updates-summary.png":::

This report allows you to view the status of driver updates for each policy (*Profile* column). It displays the number of devices that are up-to-date (*Success*), failed (*Error*), paused (*Paused*), etc. for the driver updates in that policy. However, each device is only represented once in a single status column, based on the worst status across all of the updates that apply to that device.

Intune ranks the following statuses in order of priority, from best (Success) to worst (NeedsReview):

- **Success** – All applicable driver updates have installed successfully.
- **In progress** – At least one update remains in progress, and none have been paused, failed, or worse.
- **Paused** – At least one update has been paused, but none have failed to install, been cancelled, or are pending review.
- **Error** – At least one update failed to install, but none are cancelled or pending review.
- **Cancelled** – At least one update has been declined, but none are pending review.
- **NeedsReview** – One or more updates are new to the policy and pending review to approve or decline.

For example: A policy might have three applicable driver updates for an assigned device. If one of the three fails to install on that device while the other two updates install successfully, the device is identified by adding one to the *Error* column. Once all three updates install successfully, the device is represented by adding one to the *Success* column and reducing the count of the *Error* column by one.

This report doesn't support drilling in for more details about devices, driver updates, or policy details.

## Windows Driver updates report

The *Windows Driver Updates report* allows you to select a single driver update and view details about the policies in which it's applicable for a device. This report provides information about the driver from all your driver update policies, offering a different perspective than other reports, which only provide details specific to a single policy.

To find this report, in the admin center go to **Reports** > **Windows updates** > **Reports** tab, and then select the **Windows Driver Update Report** tile.

In the following screen capture, the report shows details for the driver update *Microsoft – APPLIANCES – 1.0.0.1*.

:::image type="content" source="./images/reports/report-driver-updates-drivers.png" alt-text="Screen capture of the Windows Driver updates report." lightbox="./images/reports/report-driver-updates-drivers.png":::

To change the focus of this report to a different driver:

1. On the **Windows Driver updates** view, select **Select a driver update** to open the **Driver updates** pane on the right.

2. The *Driver updates* pane displays a list of updates that are approved and applicable for at least one device from across all your driver update policies.

3. On the Driver updates pane, select a driver, and then **OK** to return to the Windows Driver updates report view that now shows information for the driver you selected, and select **Generate again** to update the report.

In the following screen capture, only four drivers remain applicable to devices with driver updates policy, and those four updates are different versions of the same driver update.

:::image type="content" source="./images/reports/report-driver-updates-pane.png" alt-text="Screen capture of Driver Updates pane of a driver updates policy." lightbox="./images/reports/report-driver-updates-pane.png":::

**Column details**:

While most of the column details should be clear, the following warrant some explanation:

- **Update State** – This column presents the most recent status of the selected driver update, as reported by each device to which it applies. Further details can be found in the *Update Substrate* column.

  - **Cancelled** – The update was paused in the policy that applies to this device.
  - **Offering** – The update is approved, but the device hasn't yet installed it.
  - **Installed** – The update installed successfully.
  - **Needs attention** – There's an installation issue for the update on this device.

- **Policy** – This column identifies the name of the policy in which the update was approved.

- **Last Scan Time** – This column provides insight into when a device last checked for updates. This can help explain why approved updates haven't installed. For instance, if the last scan time is several weeks old, it may indicate that the device is either offline or unable to connect to scan for updates.

**Data retention**:

As devices across all your updates policies install the latest versions of a driver update, older driver update versions that are no longer needed by any device drops off the driver updates list. However, this isn't necessarily an immediate event. Reporting data for driver updates remains available until the end of a data retention period is reached. This period is six months since the last time an event for the update is received.

- If the update is approved and all applicable devices have installed the update, then six months after the last device updates is status, the update is removed from reporting details.
- Similarly, if an update is paused and shows no activity for the retention period, that update is also dropped from reporting details after six months. After an updates data ages out, if a paused update that remains applicable to a device is reapproved, subsequent status for that update begins to appear in reports. Previous data that aged out of reports won't be restored or available.

## Windows Driver update failures

Windows driver updates include a report on driver update failures. To find this report, in the admin center go to **Devices** > **Monitor** > **Windows Driver update failures**. This report is part of the *Software updates* group and might require you to scroll down the admin center to locate it.

:::image type="content" source="./images/reports/report-driver-updates-failures.png" alt-text="Screen capture of the Windows Driver update failure report." lightbox="./images/reports/report-driver-updates-failures.png":::

When you select the report, you can view a list of your update policies and see a count of devices in each policy that have at least one driver update error. In the previous screen capture, only one driver has such an error.

By selecting that policy and entry, you can then view more information about the error, including:

- Device Name
- Driver Name
- Driver Class
- Alert Message
- Deployment Error Code
- UPN
- Intune Device ID

This view is a useful place to identify and start investigation of driver update installation failures.

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431