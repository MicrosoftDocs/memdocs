---
title: Advanced Analytics overview
description: Discover what Microsoft Intune Advanced Analytics is, how it extends endpoint analytics with advanced device insights, proactive troubleshooting, and enhanced reporting.
ms.date: 12/01/2025
ms.topic: concept-article
---

# Advanced Analytics overview

Microsoft Intune Advanced Analytics delivers deep, actionable insights into the health and performance of your organization's endpoints. Built on the foundation of [endpoint analytics](../endpoint-analytics/index.md), it helps IT teams proactively manage user experience and optimize productivity through data-driven intelligence. By turning raw telemetry into meaningful insights, Advanced Analytics reduces support costs, accelerates problem resolution, and ensures a more reliable technology experience for every user.

## Availble reports and capabilities

Advanced Analytics enhances endpoint analytics with the following reports and capabilities:

:::row:::
:::column:::  
#### :::image type="icon" source="../media/icons/24/report.svg"::: Resource performance report

> Identify CPU and RAM performance issues by device, model, and manufacturer to guide future purchasing decisions.
> 
> > [!div class="nextstepaction"]
> > [Learn more](resource-performance.md)
:::column-end:::
:::column:::
#### :::image type="icon" source="../media/icons/24/report.svg"::: Battery health report

> Monitor battery health for Windows devices to ensure long battery life and a better user experience.
> 
> > [!div class="nextstepaction"]
> > [Learn more](battery-health.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::
#### :::image type="icon" source="../media/icons/24/report.svg"::: Anomalies report

> Track device health for regressions in user experience and productivity after configuration changes.
>
> > [!div class="nextstepaction"]
> > [Learn more](anomalies.md)
:::column-end:::
:::column:::
#### :::image type="icon" source="../media/icons/24/report.svg"::: Device timeline report

> Provides more event details and lower data latency to help troubleshoot device issues.
> 
> > [!div class="nextstepaction"]
> > [Learn more](device-timeline.md)
:::column-end:::


:::row-end:::

:::row:::
:::column:::  
#### :::image type="icon" source="../media/icons/24/query.svg"::: Device query

> Get near-real time access to data about the state and configuration of Windows devices.
> 
> > [!div class="nextstepaction"]
> > [Learn more](device-query.md)
:::column-end:::
:::column:::
#### :::image type="icon" source="../media/icons/24/query.svg"::: Device query for multiple devices

> View collected inventory data across multiple devices and platforms.
> 
> > [!div class="nextstepaction"]
> > [Learn more](device-query-multiple-devices.md)
:::column-end:::
:::row-end:::
:::row:::
:::column:::  
#### :::image type="icon" source="../media/icons/24/devices.svg"::: Device scopes

> Use scope tags to filter endpoint analytics reports for a subset of devices. See scores, insights, and recommendations specific to those devices.
> 
> > [!div class="nextstepaction"]
> > [Learn more](device-scopes.md)
:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

## Prerequisites

To use Advanced Analytics features, devices must meet the [endpoint analytics prerequisites](../endpoint-analytics/index.md#prerequisites) and you must [configure endpoint analytics](../endpoint-analytics/configure.md) in your tenant.

This section details **additional prerequisites** specific to Advanced Analytics. Certain features may have their own additional prerequisites; see the individual feature articles for more information.

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
>   > Support for Advanced Analytics in GCC High and DoD environments doesn't include the [*Device query*](device-query.md) functionality or [*Resource performance*](resource-performance.md) report.
>   For more information, see [Microsoft Intune for US Government GCC service description](../intune-service/fundamentals/intune-govt-service-description.md).

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> Advanced Analytics features support Windows devices that are:
>
> - Managed by Intune
> - Co-managed (Intune + Configuration Manager)
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

> Advanced Analytics features are included in [Microsoft Intune Suite](../intune-service/fundamentals/intune-add-ons.md). The capabilities are also available as an individual add-on to Microsoft subscriptions that include Intune.
>
> **Mixed licensing scenarios**: A mixed licensing scenario occurs when some users in your tenant have access to Advanced Analytics through an add-on subscription or trial, while others only have access to the *base* endpoint analytics product. In these cases, the subscription with the highest level of functionality determines the overall endpoint analytics experience for your tenant. For example, if any users have Advanced Analytics, all enrolled devices will benefit from the advanced features.
:::column-end:::
:::row-end:::

## Get started with Advanced Analytics

Before deploying Advanced Analytics, complete these foundational tasks:

- Assess your organization's privacy and compliance requirements for device data. Review the Intune [data platform schema](data-platform-schema.md) to understand which data is captured.
- Define escalation and support procedures for handling analytics findings.
- Train staff on IT processes you plan to optimize, such as help desk triage, hardware refresh cycles, and app updates. Treat this as a continuous improvement cycle for faster and more proactive issue resolution.

### Enable Advanced Analytics

When license requirements are met, then Advanced Analytics capabilities are automatically enabled in your tenant.

>[!NOTE]
> It might take up to 48 hours after you buy licenses or start a trial to see Advanced Analytics features in your tenant.

For the extra reports and capabilities on Windows devices:
- Devices must to be enrolled into Intune and onboarded to endpoint analytics.
- [Device query for multiple devices](device-query-multiple-devices.md) requires a properties catalog policy to be configured and deployed.

### Advanced Analytics in the Intune admin center

Advanced Analytics is built into Microsoft Intune and appears in the **Reports** > **Endpoint analytics** section, as well as other areas of the Intune admin center. When enabled, it adds the following enhancements:

- Endpoint analytics reports are extended with:
  - [Resource performance report](resource-performance.md)
  - [Battery health report](battery-health.md)
  - [Anomalies report](anomalies.md)
  - [Device scopes](device-scopes.md)
- Single device views are extended with:
  - [Battery health report](battery-health.md)
  - [Device timeline report](device-timeline.md), which replaces the [application reliability report](../endpoint-analytics/app-reliability.md)
  - [Resource performance report](resource-performance.md)
  - [Device query](device-query.md)
- Additional capabilities:
  - [Device query for multiple devices](device-query-multiple-devices.md) under the **Devices** node in the Intune admin center

### Integrate Advanced Analytics into business processes

After completing the setup tasks, follow these steps to embed Advanced Analytics into daily operations:

1. **Update support processes** to:
   - Use the [device timeline report](device-timeline.md) to identify patterns, such as restarts or updates linked to anomalies.
   - Use [device query](device-query.md) to retrieve live device data for troubleshooting.
1. **Schedule regular reviews** of:
   - [Anomalies reports](anomalies.md) after OS or app updates to catch issues early.
   - [Battery health reports](battery-health.md) to identify devices needing attention for better performance and user experience.
   - [Resource performance reports](resource-performance.md) to track performance by device, model, and manufacturer—helpful for future purchasing decisions.