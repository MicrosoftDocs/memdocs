---
title: What is Microsoft Intune Advanced Analytics
description: Discover what Microsoft Intune Advanced Analytics is, how it extends endpoint analytics with advanced device insights, proactive troubleshooting, and enhanced reporting.
ms.date: 10/09/2025
ms.topic: concept-article
---

# What is Microsoft Intune Advanced Analytics

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

Microsoft Intune Advanced Analytics provides comprehensive visibility of the end-user experience in your organization and optimizes it with data driven insights. With Intune Advanced Analytics, your organization can proactively detect and resolve endpoint issues, streamline troubleshooting process, and improve your users' technology experience.

Advanced Analytics includes the following features:

:::row:::
:::column span="1":::
- **[Anomaly detection](anomaly-detection.md)**
:::column-end:::
:::column span="3":::
>Monitors the health of devices in your organization for user experience and productivity regressions following configuration changes.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
- **[Battery health](battery-health.md)**
:::column-end:::
:::column span="3":::
>Report helps you understand the battery health of your Windows devices to ensure long battery life and good user experience.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
- **[Device scopes](device-scopes.md)**
:::column-end:::
:::column span="3":::
>Use [Scope tags](../intune-service/fundamentals/scope-tags.md) to slice endpoint analytics reports to a subset of devices. See scores, insights, and recommendations specific to subsets of your enrolled devices. For example,  you can focus on devices that you manage, devices assigned to a specific business group, or devices located in a particular geographic region.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
- **[Enhanced device timeline](enhanced-device-timeline.md)**
:::column-end:::
:::column span="3":::
>Includes more events and lower data latency to assist with troubleshooting device issues
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
- **[Resource Performance](resource-performance-report.md)**
:::column-end:::
:::column span="3":::
> Report to identify challenges with resource performance by device, model, and manufacturer to aid in future purchasing decisions.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
- **[Device query](device-query.md)**
:::column-end:::
:::column span="3":::
> Get near-real time access to data about the state and configuration of devices.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
- **[Device query for multiple devices](device-query-multiple-devices.md)**
:::column-end:::
:::column span="3":::
> View collected inventory data across multiple devices and platforms.
:::column-end:::
:::row-end:::

## Advanced Analytics Reports

Intune Advanced Analytics is automatically integrated into the existing base endpoint analytics experience in the Intune admin center under **Reports** > **Endpoint analytics**.

When Advanced Analytics is enabled, endpoint analytics reports are supplemented with:

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


## Prerequisites

Intune Advanced Analytics features build on top of the base endpoint analytics experience, but it's only available for Intune-managed devices (including co-managed devices). Devices must meet the [endpoint analytics prerequisites](index.md#prerequisites) to use Advanced Analytics features, and must be enrolled in endpoint analytics.

This section details additional prerequisites specific to Advanced Analytics features.

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> **Single device query** requires the device to be marked as corporate.
>
> **Device query for multiple devices** is supported on devices running:
> - Windows
> - Android
>   - Android Enterprise corporate owned dedicated devices (COSU)
>   - Android Enterprise corporate owned fully managed (COBO)
>   - Android Enterprise corporate owned work profile (COPE)
> - Apple
>   - iOS/iPadOS
>   - macOS
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> Advanced Analytics supports Windows devices that are:
>
> - Managed by Intune
> - Co-managed (Intune + Configuration Manager)
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined
>
> **Single device query** requires the device to be marked as corporate.
>
> **Device query for multiple devices** requires a [properties catalog policy](/intune/intune-service/configuration/properties-catalog) to be configured and deployed.
>
> [!NOTE]
> For iOS/iPadOS, Android, and macOS, data is automatically collected and a separate properties catalog policy doesn't need to be deployed.

:::column-end:::
:::row-end:::

## Next Steps

> [!div class="nextstepaction"]
> [Next: Plan Advanced Analytics >](plan.md)

---

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)
