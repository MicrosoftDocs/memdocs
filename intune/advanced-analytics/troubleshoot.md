---
title: Advanced Analytics Troubleshooting and Frequently Asked Questions
description: Find troubleshooting steps and FAQs for Microsoft Intune Advanced Analytics, including endpoint analytics issues, data refresh, and dashboard customization.
ms.date: 10/09/2025
ms.topic: faq
---

# Advanced Analytics Troubleshooting and Frequently Asked Questions

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

[!INCLUDE [advanced-analytics-overview](includes/advanced-analytics-overview.md)]

## Frequently Asked Questions

### What is the difference between endpoint analytics and Advanced Analytics?

Advanced Analytics builds on endpoint analytics by offering deeper insights, advanced reporting, and enhanced anomaly detection capabilities.

### Do I need additional licensing for Advanced Analytics?

Yes, Advanced Analytics requires specific licensing. See the Plan section for details.

### Can Advanced Analytics integrate with other monitoring tools?

Advanced Analytics doesn't provide a connector for data to be leveraged in other monitoring tools. Some features, such as Device Query for multiple devices, do support an export via .csv function, which could then be used in other tooling.

### Are there limitations with device types or OS versions?

Some advanced features may be limited to specific Windows builds or device types. Review prerequisites before deployment.

### Why do some crashes or anomalies sometimes not appear in Anomaly Detection, even when the devices are correctly licensed and enrolled?

This is typically due to the volume and usage patterns of devices and apps. The device must be actively used, enrolled in endpoint analytics, and data collection is enabled. In addition, a high volume of events (such as BSODs or app crashes) is usually required before the event is flagged as anomalous.

### How often is analytics data refreshed?

Data is typically updated every 24 hours. Real-time troubleshooting may require direct device queries.

### Can I customize analytics dashboards?

Yes, dashboards can be tailored to highlight key metrics and device scopes relevant to your organization.

### What should I do if a device is not reporting data?

Check device connectivity, enrollment status, and compliance with system requirements.

### How should the baselines be used?

Baseline scores are shown on charts as triangle markers. There's a built-in baseline for All organizations (median), which allows you to compare your scores to a typical enterprise. You can create new baselines based on your current metrics so you can track progress or view regressions over time.

## Troubleshooting

### Analytics Data Not Updating

Ensure devices are online and have connectivity to required Microsoft endpoints. Verify data collection settings and licensing status. Devices will need to restart at least once after the policy arrives for data to properly display.

### Incomplete Device Reports

Check that targeted devices meet the [prerequisites](plan.md#prerequisites). In some cases, end-to-end latency might exceed 24 hours when event details aren't able to upload from the client right away. Events such as restarts and stop errors experience this when the device doesn't immediately reboot after the shut-down or stop error event. In this case, the event details are uploaded at the next available opportunity, and the event appears on the timeline with a timestamp equal to the time the event occurred.

---

## Next Steps

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)
