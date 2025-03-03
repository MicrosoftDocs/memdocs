---
title: Enhanced device timeline in Endpoint analytics
titleSuffix: Microsoft Endpoint Manager
description: Learn about Enhanced device timeline as an Advanced Analytics feature in Intune
ms.date: 01/26/2024
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: article
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---
# Enhanced device timeline in Endpoint analytics

> [!NOTE]
> This capability is available as an Intune add-on. For more information, see [Intune add-ons](../intune/fundamentals/intune-add-ons.md).

The enhanced device timeline allows you to see a history of events that have occurred on a specific device. When you're viewing a specific device in Endpoint analytics, the enhanced device timeline is viewable on the **Device timeline** tab.

:::image type="content" source="media/enhanced-device-timeline.png" alt-text="Enhanced device timeline in endpoint analytics" lightbox="media/enhanced-device-timeline.png":::

> [!NOTE]
> The **Device timeline** tab replaces the **Application reliability** tab in tenants that have Advanced Analytics features in Intune.

You can search by event name or details. Select the **Add filter** button to choose the source and level of events that appear on the device timeline and select a time range of interest.  

Currently, the enhanced device timeline contains app crash, app unresponsive, device boot, device logon, and anomaly detected events. The end-to-end latency is generally under 24 hours.  

> [!NOTE]
> In some cases, end-to-end latency may exceed 24 hours when event details are not able to upload from the client right away. This is most common for events such as restarts and stop errors when the device does not immediately reboot after the shut down or stop error event. In this case, the event details will upload at the next available opportunity, and the event will appear on the timeline with a timestamp equal to the time the event occurred.

> [!NOTE]
> Event timestamps are localized according to the time zone of the logged on Intune user.  

## Limitations

- When your tenant has Advanced Analytics features in Intune, the enhanced **Device timeline** tab replaces the **Application reliability** tab in device drill-down views. In addition to a timeline, the **Application reliability** tab includes the application reliability score for the selected device. To see the device application reliability score, use the table on the **Device performance** tab and search for the desired device.

- As the enhanced device timeline is only available for Intune-managed (including co-managed) devices, a device timeline isn't currently available for Configuration Manager-only devices in tenants that have Advanced Analytics features in Intune.

## Next Steps

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [What is Intune Advanced Analytics](advanced-endpoint-analytics.md)
- [Battery health](battery-health.md)
