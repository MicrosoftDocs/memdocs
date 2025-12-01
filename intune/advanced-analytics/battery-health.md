---
title: Battery Health Report in Advanced Analytics
description: Learn how the battery health report in Microsoft Intune Advanced Analytics provides insights into device battery performance, degradation, and proactive replacement strategies.
ms.date: 12/01/2025
ms.topic: concept-article
---

# Battery health report

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

The battery health report provides visibility into the health of batteries in your organization's devices and its influence on user experience.

The score helps you identify emerging hardware issues that might be impacting user productivity so you can proactively make improvements before users generate support tickets.

The insights show how much your score can improve by replacing batteries in affected devices. They also help you identify quickly failing batteries that can be replaced under warranty before they expire.

The battery health report can be used to:

- Plan battery replacements proactively to reduce downtime and improve user experience.
- Identify devices with poor battery still under warranty, and proactively repair/replace them.
- For devices with high battery capacity scores, review their associated resource performance report and consider extending their lifecycle usage to reduce costs.

## Before you begin

Make sure you meet the [requirements](index.md#prerequisites) before using the battery health report.

## Review the battery health report

1. In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Endpoint analytics** > **Battery health**.
1. The Battery health report page is divided in multiple tabs. Select the following tabs to learn more about them:

# [**Overview**](#tab/overview)

:::image type="content" source="images/battery-health/battery-health.png" lightbox="images/battery-health/battery-health.png" alt-text="Screenshot of the Battery Health tab in Advanced analytics.":::

### Battery Health Score

The battery health score gives an overview of laptop battery health. It's calculated as a weighted average of your organization's battery capacity score and battery runtime score, helping you identify batteries that need replacement.

The maximum capacity of a battery is the ratio of its full charge capacity against its design capacity. The full charge capacity shows the Watt-hours the battery can hold on a full charge now, while the design capacity shows the Watt-hours the battery could hold when it was new. For example, a maximum capacity of 50% on a battery with design capacity of 70 Watt-hours means that the battery now holds only 35 watt-hours on a full charge.

**Battery capacity score**: Based on the maximum capacities of batteries in your organization's devices, we create a score from 0 (poor) to 100 (exceptional). Your battery capacity score is the average for all devices.

The *estimated device runtime* is an estimate of the amount of time a device runs using a battery on full charge and assuming the system's usage pattern is comparable to when the device was plugged in. The *Battery capacity score* is calculated from the combined battery capacity and estimated battery drain rate.

**Battery runtime score**: Based on the estimated device runtimes for batteries in your organization's devices, we create a score from 0 (poor) to 100 (exceptional). Your battery runtime score is the average for all devices.

### Insights and recommendations

The Battery health page provides a prioritized list of Insights and recommendations, described in this section:

**Low battery capacity**: These devices have batteries that hold less charge compared to what they were designed to hold. Devices with battery capacities below 60% are considered most impacted whereas devices with battery capacities between 60-80% are considered moderately impacted. The insights might contain one of these conditions independently or in combination with low runtimes.

For example, some devices might have batteries with below 60% capacity but still provide reasonable runtimes because their design capacities are high. Whereas other devices might have batteries with below 60% capacity and less than 3 hours of runtime, in which case they're a part of insights that highlight both gaps together.

**Low estimated runtime**: These devices result in poor user experience as they must be plugged in frequently. Devices with battery estimated runtimes below 3 hours are considered most impacted. Low runtimes are typically reported in combination with battery capacities.

Devices with less than 3 hours of runtime usually have poor maximum capacities and are included in insights that highlight both issues together. The exception is seen in the following scenario where even with high capacities, the batteries drain quickly because of power hungry apps. Either by design or because of poor energy usage efficiency.

**Good battery capacity but poor runtime**: Estimated runtimes might be low despite batteries having good maximum capacities. Low runtime is possible in two scenarios:

1. The device is running apps that drain the battery quickly. Users run applications that consume high power or inefficiently use power and need upgrading or replacing. Battery-powered devices can use the [battery saver Windows](/windows-hardware/design/component-guidelines/battery-saver) feature to ensure that both user productivity and experience are protected.
1. The device has a battery that is designed to hold low charge. Procurement teams drive this decision.

Insights for this scenario highlight the devices for which the **App Impact** tab might provide more visibility into whether the user needs to use power hungry apps or whether the app's battery usage is unusually high due to inefficiency.

# [**Device performance**](#tab/dev-perf)

This tab provides battery health metrics and a score for all your battery-powered devices. You can sort by a particular metric (for example, **Max capacity**) to see which battery-powered devices have the worst scores for that metric to help with troubleshooting. You can also search for a battery-powered device by name. If you select a battery-powered device, you can see its runtime trend, its score vis-à-vis the model's average score in the organization, and the top apps that consumed its battery in the last 14 days. These details can help you identify any corrective actions needed to improve the user experience.

The cycle count is the number of times the battery discharges 100% of its capacity, but not necessarily at one time. For example, if a battery discharges 50% of its capacity on day 1, 30% on day 2, and 20% on day 3, then its cycle count goes up by 1 after these three days.

# [**Model performance**](#tab/model-perf)

This tab shows battery health metrics and scores by device models, helping you identify if problems are specific to certain models.

# [**OS performance**](#tab/os-perf)

This tab lets you see the battery health metrics and scores by operating system versions, which can help you identify whether problems are isolated to particular OS versions.

# [**App impact**](#tab/app-impact)

This tab lets you see the organization's cumulative battery usage per app in the last 14 days. You can see the number of battery-powered devices for which the associated battery usage of an app and the percentage of the cumulative battery charge that the app consumed is recorded. This information helps to troubleshoot apps that might be consuming an inordinate amount of battery.

> [!NOTE]
> The battery power used by an app varies by the activity that a user engages in. For example, using Microsoft Teams for chatting vs in an audio/video call with screen share results in different battery drains. The data in the *App impact* tab accounts for all activity using an app.

---

## Battery information notes

- Estimated runtimes may be unavailable for battery-powered devices when there isn't enough data on battery drain.
- If the battery design doesn't report cycle count, that information won't appear in the report.
- For new batteries, limited data may result in a cycle count of `0*` (zero with an asterisk).
- In rare cases, the battery count may exceed 2, which usually means the device is connected to a UPS or external batteries. Because this is unusual, an asterisk (`*`) is added when the count is greater than 2.

## Limitations

- Some data points in the report may display **Not available**. When you export the report, unavailable data appears as `-1` in the generated .csv file.
- Devices with batteries designed for low capacity (for example, those intended to hold a limited charge) will show low runtime. This behavior is by design. These devices appear under low-runtime insights, and the only way to improve runtime is to replace the battery with one that supports a higher capacity.

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431