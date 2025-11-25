---
title: Advanced Analytics overview
description: Discover what Microsoft Intune Advanced Analytics is, how it extends endpoint analytics with advanced device insights, proactive troubleshooting, and enhanced reporting.
ms.date: 10/09/2025
ms.topic: concept-article
---

# Advanced Analytics overview

Microsoft Intune Advanced Analytics provides comprehensive visibility of the user experience in your organization and optimizes it with data-driven insights. With Advanced Analytics, your organization can proactively detect and resolve endpoint issues, streamline troubleshooting process, and improve your users' technology experience.

Advanced Analytics features build on top of the base endpoint analytics experience, but it's only available for Intune-managed devices (including co-managed devices).

## Advanced Analytics features

Advanced Analytics includes the following features:

:::row:::
:::column:::
#### Anomaly detection

> Monitors the health of devices in your organization for user experience and productivity regressions following configuration changes.

> [!div class="nextstepaction"]
> [Learn more](anomaly-detection.md)
:::column-end:::
:::column:::
#### Battery health

> Report that helps you understand the battery health of your Windows devices to ensure long battery life and good user experience.

> [!div class="nextstepaction"]
> [Learn more](battery-health.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::  
#### Device query

> Get near-real time access to data about the state and configuration of Windows devices.

> [!div class="nextstepaction"]
> [Learn more](device-query.md)
:::column-end:::
:::column:::
##### Device query for multiple devices

> View collected inventory data across multiple devices and platforms.

> [!div class="nextstepaction"]
> [Learn more](device-query-multiple-devices.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::  
#### Device scopes

> Use scope tags to slice endpoint analytics reports to a subset of devices. See scores, insights, and recommendations specific to subsets of your enrolled devices.

> [!div class="nextstepaction"]
> [Learn more](device-scopes.md)
:::column-end:::
:::column:::
##### Enhanced device timeline

> Includes more events and lower data latency to assist with troubleshooting device issues.

> [!div class="nextstepaction"]
> [Learn more](enhanced-device-timeline.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::  
#### Resource Performance

> Report to identify challenges with resource performance by device, model, and manufacturer to aid in future purchasing decisions.

> [!div class="nextstepaction"]
> [Learn more](resource-performance-report.md)
:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

## Prerequisites

Devices must meet the [endpoint analytics prerequisites](index.md#prerequisites) to use Advanced Analytics features, and must be onboarded to endpoint analytics.

This section details **additional prerequisites** specific to Advanced Analytics features.

:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::

> - Public cloud
> - Sovereign cloud environments:
>   - U.S. Government Community Cloud (GCC) High
>   - U.S. Department of Defense (DoD)
>   > [!NOTE]
>   >
>   > Support for Advanced Analytics in GCC High and DoD environments doesn't include the [*Device query*](device-query.md) or [*Resource performance*](resource-performance-report.md) functionality.
>   For more information, see [Microsoft Intune for US Government GCC service description](../intune-service/fundamentals/intune-govt-service-description.md).

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
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
> **Device query for multiple devices** requires a [properties catalog policy](/intune/intune-service/configuration/properties-catalog) to be configured and deployed.
>
> [!NOTE]
> For iOS/iPadOS, Android, and macOS, data is automatically collected and a separate properties catalog policy doesn't need to be deployed.

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

> Advanced Analytics features are included in [Microsoft Intune Suite](../intune-service/fundamentals/intune-add-ons.md). The capabilities are also available as an individual add-on to Microsoft subscriptions that include Intune.
>
> ### Mixed licensing scenarios
>
> A mixed licensing scenario occurs when some users in your tenant have access to Advanced Analytics through an add-on subscription or trial, while others only have access to the base endpoint analytics product.
>
>Currently, the highest functional subscription sets the endpoint analytics experience for your tenant. In the earlier example, your tenant experience would include advanced features in endpoint analytics for all enrolled devices.
:::column-end:::
:::row-end:::


### Reports available in Advanced Analytics

Intune Advanced Analytics is automatically integrated into the existing base endpoint analytics experience in the Intune admin center under **Reports** > **Endpoint analytics**.

When Advanced Analytics is enabled, endpoint analytics reports are supplemented with:

- [Anomaly detection](anomaly-detection.md)
- [Battery health](battery-health.md)
- [Resource Performance report](resource-performance-report.md)
- [Device scopes](device-scopes.md)

### Per-device features

When Advanced Analytics is enabled, single device views in Intune are supplemented with:

- [Device query](device-query.md)
- [Enhanced device timeline](enhanced-device-timeline.md)
- [Resource Performance report](resource-performance-report.md)
- [Battery health](battery-health.md)

> [!NOTE]
> The **Device timeline** tab replaces the **Application reliability** tab in tenants that have Advanced Analytics features in Intune.

### Multi-device query

When Advanced Analytics is enabled, [**Device query** for multiple devices](device-query-multiple-devices.md) is enabled under the **Devices** node in the *Intune admin center*.

## Plan for Advanced Analytics

For a successful deployment of Advanced Analytics, the following activities are recommended:

- Assess your organization's privacy and compliance requirements for device data. Review the Intune [data platform schema](data-platform-schema.md) to understand the full list of data captured.
- Establish escalation and support procedures for analytics findings.
- Review and train staff on IT processes you aim to optimize with the implementation of Advanced Analytics. Examples include help desk triage, hardware refresh cycles and application updates. Think of this as a continuous improvement cycle, with faster issue resolution and proactive issue resolution.

## Related articles

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)
