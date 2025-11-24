---
title: Advanced Analytics Troubleshooting and Frequently Asked Questions
description: Find troubleshooting steps and FAQs for Microsoft Intune Advanced Analytics, including endpoint analytics issues, data refresh, and dashboard customization.
ms.date: 10/09/2025
ms.topic: faq
---

# Advanced Analytics Troubleshooting and Frequently Asked Questions

## Analytics Data Not Updating

Ensure devices are online and have connectivity to required Microsoft endpoints. Verify data collection settings and licensing status. Devices will need to restart at least once after the policy arrives for data to properly display.

## Incomplete Device Reports

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
