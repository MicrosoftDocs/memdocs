---
title: Resource Performance Report in Microsoft Intune Advanced Analytics
description: Explore the resource performance report in Microsoft Intune Advanced Analytics for CPU and RAM insights, device performance analysis, and proactive endpoint analytics.
ms.date: 12/01/2025
ms.topic: concept-article
---

# Resource performance report

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

The resource performance report gives you a clear view of processor and memory performance on Windows devices and how these factors affect user experience. By tracking the performance score, you can spot emerging hardware issues that may reduce productivity and take proactive steps before support tickets occur.

The report also provides actionable insights—showing how much your score could improve by upgrading CPU or RAM and helping you identify devices for replacement before warranties expire.

## Before you begin

Make sure you meet the [requirements](index.md#prerequisites) before using the resource performance report.

Additional requirements information:

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> This report supports the following platforms:
> - Windows
> - Windows 365 Cloud PCs
:::column-end:::
:::row-end:::
:::row:::
:::column span="1":::
[!INCLUDE [licensing](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::
> If your organization has Windows 365 licenses, you also get access to the resource performance report for your Cloud PCs.
:::column-end:::
:::row-end:::

## Review the report

In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Endpoint analytics** > **Resource performance**.

:::image type="content" source="images/resource-perf-report/report-home.png" lightbox="images/resource-perf-report/report-home.png" alt-text="This is a screenshot of the Resource performance report page":::

The **Resource performance score** provides an overall performance rating (from 0 to 100) of CPU and RAM for your organization's Windows devices and Cloud PCs. This score is a weighted average of CPU spike time score and RAM spike time score.

This score helps identify device resources that need to be replaced to improve user experience and boost productivity.

### CPU spike time score

The CPU spike time score (from 0 to 100) is assigned based on the device's usage duration and the CPU spike time %, which is the percentage of the usage duration in which the device experiences CPU spikes. High usage and spikes indicate a poor experience with the device and result in low scores. Conversely, low spikes indicate a good experience with the device and result in high scores.

**CPU spike time %**: The daily metric trends graph plots the ratio of CPU spike times to total usage time. This CPU spike % data is averaged over a 14-day period ending on the date at the bottom of the graph.

Usage over 50% is considered a spike.

- To improve the performance of CPU in Windows devices, you could upgrade the processors by increasing the number of cores or the clock speed, optimize the operating system or adjust power settings.
- To improve the performance of CPU in Cloud PCs, you could upgrade to a higher configuration of Cloud PCs.

### RAM spike time score

The RAM spike time score (from 0 to 100) is assigned based on the device's usage duration and the RAM spike time %, which is the percentage of the usage duration in which the device experiences RAM spikes. High usage and spikes indicate a poor experience with the device and result in low scores. Conversely, low spikes indicate a good experience with the device and result in high scores.

**RAM spike time %**: The daily metric trends graph plots the ratio of RAM spike times to total usage time. This RAM spike % data is averaged over a 14-day period ending on the date at the bottom of the graph. Usage over 75% is considered a spike.

- To improve the performance of RAM in Windows physical devices, you could add more RAM, upgrade to higher-speed RAM, or modify UEFI/BIOS settings to optimize utilization.
- To improve the performance of RAM in Cloud PCs, you could upgrade to a higher configuration of Cloud PCs.

**Baseline** helps you see if you're meeting goals. You can set the baseline to the organizational median or a custom value.

**Insights and recommendations** suggest actions that you can take to improve your scores.

### Insights and recommendations

The **Resource performance page** provides a prioritized list of insights and recommendations, which are described in this section:

#### High CPU usage in physical devices

These Windows physical devices experience higher CPU spike % than the rest of the devices in your organization, resulting in poor user experience and lower productivity.

This category has two sub-categories:

- Physical devices that experience high CPU spike %.
- Physical device models that experience high CPU spike %.

Besides giving visibility into devices that aren't supporting your user's goals, these insights also allow you to identify devices with underperforming CPUs that are within warranty and eligible for replacement.

#### High RAM usage in physical devices

These Windows physical devices experience higher RAM spike % than the rest of the devices in your organization, resulting in poor user experience and lower productivity.

This category has two sub-categories: (1) physical devices that experience high RAM spike % and (2) physical device models that experience high RAM spike %.

Besides giving visibility into devices that aren't supporting your user's goals, these insights also allow you to identify devices with underperforming RAM that are within warranty and eligible for replacement.

#### Cloud PCs

These Windows 365 Cloud PCs experience higher CPU or RAM spike % than the rest of the devices in your organization, resulting in poor user experience and lower productivity.

These insights provide visibility into Cloud PCs that aren't supporting your user's goals. Upgrading these devices to a higher configuration of Cloud PCs will improve the user experience.

## Report tabs

The resource performance report includes the following tabs:

- **Device performance**: Shows CPU and RAM performance metrics and scores for all Windows physical devices and Cloud PCs.
  - Sort by a specific metric (for example, CPU spike time %) to identify devices with the lowest scores.
  - Filter devices by a metric range (for example, RAM spike time score between 0 and 40).
  Search for a device by name.
- **Model performance**: Displays CPU and RAM performance metrics and scores by device model. Use this view to determine if issues are isolated to specific models.

## Device-level details

To get details on a specific Windows device in your organization, you can select a device's name in the **Device performance** tab. You can also use the filters or search for a device to view the row corresponding to the device you're interested in learning more about.

:::image type="content" source="images/resource-perf-report/select-device.png" lightbox="images/resource-perf-report/select-device.png" alt-text="In the Device Performance tab, use filters or search for a device to view the device details":::

The device-level details page includes the CPU and RAM spike-time history over the last 14 days for which this data is available. The page also includes device details such as model, manufacturer, processor name, number of processor cores, the processor base speed, RAM, and disk type.

:::image type="content" source="images/resource-perf-report/rp-report.png" lightbox="images/resource-perf-report/rp-report.png" alt-text="This is a screenshot of device levels details":::

## Limitations

- Some data points in the report might show `--` when not available. When you export the report, data points that aren't available appear as `-1` in the generated .csv file.

- Health status appears differently in the report and the exported .csv
  - **HealthStatus .csv value**:
    - `0`: Unknown
    - `1`: Insufficient data
    - `2`: Needs attention
    - `3`: Meeting goals

- Some columns such as `ResourcePerfScore` and `TotalRamInMB` in the generated .csv file have data type *double* whereas the corresponding columns **Resource performance score** and **RAM** in the report have data type *int*.
- Column `MachineType` in the generated .csv file can take values `Physical`, `CPC`, and `Others` whereas the corresponding column **Device Type** in the report takes values *physical*, *virtual*, and *unknown* respectively.

## Best practices

- IT administrators should periodically review the resource performance dashboard, to investigate poor performing devices from CPU or RAM spikes.
- Identify cohorts of devices, either hardware type, or by groups of users, with poor performance.
- Investigate performance issues and resolutions before users report persistent problems. Use the Device Timeline and Device Query capabilities to find the root cause of issues.
- Leverage performance data to optimize hardware replacement costs, extending the life of devices with no performance problem, or replacing underperforming devices sooner for improved user experience.

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431