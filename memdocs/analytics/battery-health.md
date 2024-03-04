---
title: Battery Health report in Microsoft Intune Advanced Analytics
titleSuffix: Microsoft Intune
description: Learn about the battery health report as an advanced feature in Endpoint analytics
ms.date: 01/26/2024
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: conceptual
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high

---

# Battery health

The battery health report provides visibility into the health of batteries in your organization's devices and its influence on user experience.

The score helps you identify emerging hardware issues that might be impacting user productivity so you can proactively make improvements before users generate support tickets.

The insights show not only how much your score can improve by replacing batteries in affected devices, but also help you identify batteries that are failing quickly and can be replaced under warranty before they expire.

## Licensing Requirements

The battery health report is part of Intune Advanced Analytics features and is included as an Intune-add on under [Microsoft Intune Suite](../intune/fundamentals/intune-add-ons.md) and requires an extra cost to the licensing options that include Microsoft Intune.

## Prerequisites

In addition to the prerequisites for [Advanced Analytics](advanced-endpoint-analytics.md#prerequisites), this report also requires that devices need to be battery-powered for them to show up in this report.

For Advanced Analytics capabilities, including battery health, battery-powered devices should be either Intune-only managed or Co-managed.

After enrollment, client devices require a restart to fully enable all analytics.

> [!NOTE]
> It may take up to 48 hours after you buy licenses or start a trial to see Battery health data in your tenant.

## Battery health report

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Report** > **Endpoint analytics** > **Battery health**.
3. The Battery health report page shows an **Overview** tab, **Device performance** tab, **Model performance** tab, **OS performance** tab, and an **App impact** tab. For more information on each of the tabs, see [Reporting Tabs](#reporting-tabs).


   :::image type="content" source="media/battery-health/battery-health.png" lightbox="media/battery-health/battery-health.png" alt-text="This is a screenshot of the Battery Health tab in Advanced analytics":::

## Battery Health Score

The battery health score provides an overview of the health status of laptop's batteries and is calculated as a weighted average of your organization's battery capacity score and battery runtime score, helping you identify batteries that need to be replaced.

The maximum capacity of a battery is the ratio of its full charge capacity against its design capacity. The full charge capacity indicates the Watt-hours that the battery can now hold on a full charge whereas the design capacity indicates the Watt-hours that the battery could hold when it was brand new. For example, a maximum capacity of 50% on a battery with design capacity of 70 Watt-hours means that the battery now holds only 35 watt-hours on a full charge.

**Battery capacity score**: Based on the maximum capacities of batteries in your organization's devices, we create a score from 0 (poor) to 100 (exceptional). Your battery capacity score is the average for all devices.

The *estimated device runtime* is an estimate of the amount of time a device runs using a battery on full charge and assuming the system's usage pattern is comparable to when the device was plugged in. The *Battery capacity score* is calculated from the combined battery capacity and estimated battery drain rate.  

**Battery runtime score**: Based on the estimated device runtimes for batteries in your organization's devices, we create a score from 0 (poor) to 100 (exceptional). Your battery runtime score is the average for all devices.

## Insights

The Battery health page provides a prioritized list of Insights and recommendations, described in this section:

**Low battery capacity**: These devices have batteries that hold less charge compared to what they were designed to hold. Devices with battery capacities below 60% are considered most impacted whereas devices with battery capacities between 60-80% are considered moderately impacted. The insights might contain one of these conditions independently or in combination with low runtimes.  

For example, some devices might have batteries with below 60% capacity but still provide reasonable runtimes because their design capacities are high. Whereas other devices might have batteries with below 60% capacity and less than 3 hours of runtime, in which case they're a part of insights that highlight both gaps together.

**Low estimated runtime**: These devices result in poor user experience as they must be plugged in frequently. Devices with battery estimated runtimes below 3 hours are considered most impacted. Low runtimes are typically reported in combination with battery capacities.  

For example, devices that have lower than 3 hours of runtime typically also have poor maximum capacities and hence are included in insights that highlight both gaps together. The exception is seen in the following scenario where even with high capacities, the batteries drain quickly because of power hungry apps. Either by design or because of poor energy usage efficiency.

**Good battery capacity but poor runtime**: Estimated runtimes might be low despite batteries having good maximum capacities. Low runtime is possible in two scenarios:

1. The device is running apps that drain the battery quickly. Users run applications that are designed to use high power per unit of time or run apps that are inefficiently utilizing power and need to be upgraded or replaced. To ensure that both user productivity and experience are protected battery-powered devices can leverage the [battery saver Windows](/windows-hardware/design/component-guidelines/battery-saver) feature.

2. The device has a battery that is designed to hold low charge. Procurement teams drive this decision.  

Insights for this scenario highlight the devices for which the **App Impact** tab might provide more visibility into whether the user needs to use power hungry apps or whether the app's battery usage is unusually high due to inefficiency.

## Reporting Tabs

The Battery health page has reporting tabs that provide support for insights. The tabs are described in this section:

### Device performance tab

This tab provides battery health metrics and a score for all your battery-powered devices. You can sort by a particular metric (for example, **Max capacity**) to see which battery-powered devices have the worst scores for that metric to help with troubleshooting. You can also search for a battery-powered device by name. If you select a battery-powered device, you can see its runtime trend, its score vis-à-vis the model's average score in the organization, and the top apps that consumed its battery in the last 14 days. These details can help you identify any corrective actions needed to improve the user experience.

The cycle count is the number of times the battery has discharged 100% of its capacity, but not necessarily at one time. For example, if a battery discharges 50% of its capacity on day 1, 30% on day 2, and 20% on day 3, then its cycle count goes up by 1 after these three days.

### Model performance tab

This tab lets you see the battery health metrics and scores by battery-powered device models, which can help you identify whether problems are isolated to particular models.

### Operating systems performance tab

This tab lets you see the battery health metrics and scores by OS versions, which can help you identify whether problems are isolated to particular OS versions.

### App impact tab

This tab lets you see the organization's cumulative battery usage per app in the last 14 days. You can see the number of battery-powered devices for which the associated battery usage of an app and the percentage of the cumulative battery charge that the app consumed is recorded. This information helps to troubleshoot apps that might be consuming an inordinate amount of battery.

> [!NOTE]
> The battery power used by an app varies by the activity that a user engages in. For example, using Microsoft Teams for chatting vs in an audio/video call with screen share results in very different battery drains. The data in the *App impact* tab accounts for all activity using an app.

## Outliers

Estimated runtimes are sometimes not available for battery-powered devices where we don't have enough information on battery drains.

If the battery design doesn't report cycle count, then the report won't contain cycle count information for such battery-powered devices.

If battery is new, we might not have enough data on the cycle count in which case a zero with an asterisk appears as the cycle count.  

In rare cases, the battery count might exceed 2 and could indicate that devices might be plugged into UPS or other extraneous battery types. Since this is unusual, we indicate this by adding an asterisk (*) if the count exceeds 2.  

## Limitations

Some data points in the report might say *Not available*. When you export the report, data points that aren't available appear as "-1" in the generated .csv file.

Batteries that have low design capacity (For example, devices designed to hold limited charge) show up as having low runtime although this is by design. Such devices are counted under low runtime insights and the only solution is to replace the battery with one that holds more charge.

## Next Steps

For more information, go to:

- [What is Intune Advanced Analytics](advanced-endpoint-analytics.md)

- [Use Intune Suite add-on capabilities](../intune/fundamentals/intune-add-ons.md)

- [Device scopes](device-scopes.md)

- [Device query](device-query.md)