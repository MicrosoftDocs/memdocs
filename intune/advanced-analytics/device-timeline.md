---
title: Device Timeline Report in Advanced Analytics
description: Discover the device timeline in Microsoft Intune endpoint analytics for detailed device event history and advanced troubleshooting.
ms.date: 12/01/2025
ms.topic: concept-article
---

# Device timeline report

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

The device timeline allows you to see a history of events that have occurred on a specific device.

## Before you begin

> [!div class="checklist"]
> - Confirm that you meet the [prerequisites](index.md#prerequisites) before using the report.

## Review the device timeline report

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows**.
1. Select a device, then select **User Experience** > **Device Timeline**.
   :::image type="content" source="images/device-timeline.png" alt-text="Screenshot of the device timeline in endpoint analytics." lightbox="images/device-timeline.png":::
1. Filter events by date, device, or user to focus on relevant incidents.

> [!NOTE]
> The **Device timeline** tab replaces the **Application reliability** tab in tenants that have Advanced Analytics.

You can search by event name or details. To refine results, select **Add filter** to choose the event source, event level, and a time range of interest.

The device timeline shows events such as app crashes, unresponsive apps, device boots, sign ins, and detected anomalies. Use the timeline to correlate software updates, user actions, and system events during troubleshooting. Most events appear within 24 hours.

In some cases, events may take longer to appear if details can't upload immediately. For example, restart or stop error events might be delayed when the device doesn't reboot right away. These events upload at the next available opportunity and display the original timestamp when they occurred.

> [!NOTE]
> Event timestamps are localized to the time zone of the logged-on Intune user.

## Limitations

- If your tenant uses Advanced Analytics, the **Device timeline** tab replaces the **Application reliability** tab in device drill-down views. Unlike the timeline, the **Application reliability** tab includes the *application reliability score* for the selected device. To view this score, go to the **Device performance** tab and search for the device.
- The device timeline is available only for Intune-managed devices (including co-managed). It isn't available for Configuration Manager-only devices in tenants with Advanced Analytics enabled.

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431