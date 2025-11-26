---
title: Advanced Analytics overview
description: Discover what Microsoft Intune Advanced Analytics is, how it extends endpoint analytics with advanced device insights, proactive troubleshooting, and enhanced reporting.
ms.date: 10/09/2025
ms.topic: concept-article
---

# Advanced Analytics overview

Microsoft Intune Advanced Analytics delivers deep, actionable insights into the health and performance of your organization's endpoints. Built on the foundation of endpoint analytics, it helps IT teams proactively manage user experience and optimize productivity through data-driven intelligence. By turning raw telemetry into meaningful insights, Advanced Analytics reduces support costs, accelerates problem resolution, and ensures a more reliable technology experience for every user.

## Available features

Advanced Analytics features are available only for Intune-managed devices (including co-managed devices). The key features include:

:::row:::
:::column:::
#### Anomaly detection

> Monitors the health of devices in your organization for user experience and productivity regressions following configuration changes.
> 
> > [!div class="nextstepaction"]
> > [Learn more](anomaly-detection.md)
:::column-end:::
:::column:::
#### Battery health

> Report that helps you understand the battery health of your Windows devices to ensure long battery life and good user experience.
> 
> > [!div class="nextstepaction"]
> > [Learn more](battery-health.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::  
#### Device query

> Get near-real time access to data about the state and configuration of Windows devices.
> 
> > [!div class="nextstepaction"]
> > [Learn more](device-query.md)
:::column-end:::
:::column:::
#### Device query for multiple devices

> View collected inventory data across multiple devices and platforms.
> 
> > [!div class="nextstepaction"]
> > [Learn more](device-query-multiple-devices.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::  
#### Device scopes

> Use scope tags to slice endpoint analytics reports to a subset of devices. See scores, insights, and recommendations specific to subsets of your enrolled devices.
> 
> > [!div class="nextstepaction"]
> > [Learn more](device-scopes.md)
:::column-end:::
:::column:::
#### Enhanced device timeline

> Includes more events and lower data latency to assist with troubleshooting device issues.
> 
> > [!div class="nextstepaction"]
> > [Learn more](enhanced-device-timeline.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::  
#### Resource performance

> Report to identify challenges with resource performance by device, model, and manufacturer to aid in future purchasing decisions.
> 
> > [!div class="nextstepaction"]
> > [Learn more](resource-performance-report.md)
:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

## Integration in the Intune admin center

Advanced Analytics is built into Microsoft Intune and appears in the **Reports** > **Endpoint analytics** section, as well as other areas of the Intune admin center. When enabled, it adds the following enhancements:

- Endpoint analytics reports are extended with:
  - [Anomaly detection](anomaly-detection.md)
  - [Battery health](battery-health.md)
  - [Device scopes](device-scopes.md)
  - [Resource performance](resource-performance-report.md)
- Single device views are extended with:
  - [Battery health](battery-health.md)
  - [Device query](device-query.md)
  - [Device timeline](enhanced-device-timeline.md)
  - [Resource performance](resource-performance-report.md)
- Additional capabilities:
  - [Device query for multiple devices](device-query-multiple-devices.md) under the **Devices** node in the Intune admin center

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
>   > Support for Advanced Analytics in GCC High and DoD environments doesn't include the [*Device query*](device-query.md) or [*Resource performance*](resource-performance-report.md) functionality.
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

For a successful deployment of Advanced Analytics, the following activities are recommended:

- Assess your organization's privacy and compliance requirements for device data. Review the Intune [data platform schema](data-platform-schema.md) to understand the full list of data captured.
- Establish escalation and support procedures for analytics findings.
- Review and train staff on IT processes you aim to optimize with the implementation of Advanced Analytics. Examples include help desk triage, hardware refresh cycles and application updates. Think of this as a continuous improvement cycle, with faster issue resolution and proactive issue resolution.

### Integrate Advanced Analytics into your business

1. Update role based access control for custom roles to include new permissions such as **Managed Devices** > **Query** for [Device Query](device-query.md). For more information, see [Role-based access control](../intune-service/fundamentals/role-based-access-control.md)
1. Update support processes to:
    1. Use [device timeline](enhanced-device-timeline.md) to review if there's a specific pattern, such as a device restart or update tied to the anomaly.
    1. Use [device query](device-query.md) retrieve live information from a device to aid troubleshooting.

1. Implement processes to periodically review:
    1. [Anomaly Detection Data](anomaly-detection.md). For example, after application or operating system updates are applied to proactively identify issues.
    1. [Battery health data](battery-health.md) to identify devices that may need attention to ensure long battery life and good user experience.
    1. [Resource performance reports](resource-performance-report.md) to identify challenges with resource performance by device, model, and manufacturer to aid in future purchasing decisions.
