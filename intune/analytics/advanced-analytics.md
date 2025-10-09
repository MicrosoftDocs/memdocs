---
title: What is Microsoft Intune Advanced Analytics
titleSuffix: Microsoft Intune
description: Learn about Intune Advanced Analytics
ms.date: 08/01/2024
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: concept-article
author: MandiOhlinger
ms.author: mandia
manager: laurawi
---

# What is Microsoft Intune Advanced Analytics

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

Microsoft Intune Advanced Analytics provides comprehensive visibility of the end-user experience in your organization and optimizes it with data driven insights. With Intune Advanced Analytics, your organization can proactively detect and resolve endpoint issues, streamline troubleshooting process, and improve your users' technology experience.

Advanced Analytics includes the following features:

- **Anomalies** monitors the health of devices in your organization for user experience and productivity regressions following configuration changes. For more information, see [Anomaly detection](anomaly-detection.md).

   :::image type="content" source="media/advanced-analytics/anomalies-tab.png" lightbox="media/advanced-analytics/anomalies-tab-expanded.png" alt-text="Screenshot of the Anomaly tab in Overview section of Endpoint analytics":::

- **Battery health** report helps you understand the battery health of your Windows devices to ensure long battery life and good user experience. For more information, see [Battery health](battery-health.md).

   :::image type="content" source="media/advanced-analytics/battery-health.png" lightbox="media/advanced-analytics/battery-health-expanded.png" alt-text="Screenshot of the Battery Health tab in Advanced analytics":::

- **Custom device scopes** allow you to use [Scope tags](../intune-service/fundamentals/scope-tags.md) to slice Endpoint analytics reports to a subset of devices. You can see scores, insights, and recommendations specific to subsets of your enrolled devices. For example,  you can focus on devices that you manage, devices assigned to a specific business group, or devices located in a particular geographic region. For more information, see [Device scopes](device-scopes.md).

- An **Enhanced device timeline** includes more events and lower data latency to assist with troubleshooting device issues. For more information, see [Enhanced device timeline](enhanced-device-timeline.md).

   :::image type="content" source="media/advanced-analytics/enhanced-device-timeline.png" alt-text="Screenshot of Enhanced device timeline in endpoint analytics" lightbox="media/advanced-analytics/enhanced-device-timeline-expanded.png":::

- A **Resource Performance** report to identify challenges with resource performance by device, model, and manufacturer to aid in future purchasing decisions. For more information, see [Resource Performance report](resource-performance-report.md).

   :::image type="content" source="media/advanced-analytics/report-home.png" lightbox="media/advanced-analytics/report-home-expanded.png" alt-text="Screenshot of the Resource performance report page":::

- **Device query** enables you to get near-real time access to data about the state and configuration of devices. For more information, see [Device query](device-query.md).

- **Device query for multiple devices** enables you to view collected inventory data across multiple devices and platforms. For more information, see [Device query for multiple devices](device-query-multiple-devices.md).

## Advanced Analytics Reports

Intune Advanced Analytics is automatically integrated into the existing base Endpoint analytics experience in the Intune admin center under **Reports** > **Endpoint analytics**.

When Advanced Analytics is enabled, Endpoint Analytics reports are supplemented with:

- [Anomaly detection](anomaly-detection.md)
- [Battery health](battery-health.md)
- [Resource Performance report](resource-performance-report.md)
- [Device scopes](device-scopes.md)

## Advanced Analytics Per-Device Features

When Advanced Analytics is enabled, single device views in Intune are supplemented with:

- [Device query](device-query.md)
- [Enhanced device timeline](enhanced-device-timeline.md)
- [Resource Performance report](resource-performance-report.md)
- [Battery health](battery-health.md)

> [!NOTE]
> The **Device timeline** tab replaces the **Application reliability** tab in tenants that have Advanced Analytics features in Intune.

## Advanced Analytics multi-device query

When Advanced Analytics is enabled, [**Device query** for multiple devices](device-query-multiple-devices.md) is enabled under the **Devices** node in the *Intune admin center*.

---

## Next Steps

> [!div class="nextstepaction"]
> [Next: Plan Advanced Analytics >](advanced-analytics-plan.md)

---

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)
