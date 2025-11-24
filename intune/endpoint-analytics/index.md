---
title: Endpoint analytics overview
description: Discover how Microsoft Intune endpoint analytics provides actionable insights to optimize device performance, improve user experience, and enable proactive IT troubleshooting.
ms.date: 10/09/2025
ms.topic: overview
zone_pivot_groups: manage-intune-cm
---

# Endpoint analytics overview

Endpoint analytics helps IT professionals assess and improve the user experience across managed devices. It provides data-driven insights into device performance, startup times, app reliability, and battery health—empowering IT teams to proactively identify and remediate issues that impact productivity.

Endpoint analytics contributes to the technology experiences category within [Microsoft Adoption Score](/microsoft-365/admin/productivity/productivity-score), offering device-level insights that complement broader organizational productivity metrics.

The service integrates with Microsoft Intune, enabling IT pros to:

- Enroll devices directly from Intune.
- Use Configuration Manager for co-managed environments.
- Manage data collection and configuration.
- View analytics in the Intune admin center.
- Apply remediations or adjust policies based on insights.

:::image type="content" source="images/ea-overview.png" alt-text="Screenshot of the endpoint analytics overview page" lightbox="images/ea-overview.png" border="false":::

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> Endpoint analytics supports the following Windows editions:
>
> - Pro
> - Pro Education
> - Enterprise
> - Education
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> Endpoint analytics supports devices that are:
>
> - Managed by Intune
> - Co-managed (Intune + Configuration Manager)
> - Managed by Configuration Manager (via tenant attach)
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined
>
> Devices must also meet the following requirements:
> - The **Connected User Experiences and Telemetry** service (DiagTrack) must be enabled and running.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [network-connectivity](../includes/requirements/network-connectivity.md)]

:::column-end:::
:::column span="3":::
::: zone pivot="intune"
>To enroll Intune-managed devices to endpoint analytics, they need to send required functional data to Microsoft public cloud. Ensure the following endpoints are accessible from Intune-managed devices:
>
> | Endpoint  | Function  |
> |-----------|-----------|
> | `https://*.events.data.microsoft.com` | Used by managed devices to send [required functional data](data-collection.md#data-collection) to the Intune data collection endpoint. |
>
>For more information and troubleshooting proxy configurations, see [Troubleshoot endpoint analytics](troubleshoot.md#proxy-server-authentication).
::: zone-end

::: zone pivot="cm"

>Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they don't need directly access to the Microsoft public cloud. If your environment uses a proxy server, configure the proxy server to allow the following endpoints:
>
> | Endpoint  | Function  |
> |-----------|-----------|
> | `https://graph.windows.net` | Used to automatically retrieve settings  when attaching your hierarchy to endpoint analytics on Configuration Manager Server role. For more information, see [Configure the proxy for a site system server](../configmgr/> core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
> | `https://*.manage.microsoft.com` | Used to synch device collection and devices with endpoint analytics on Configuration Manager Server role only. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
>
>If you have co-management enabled, enrolled devices send required functional data directly to Microsoft public cloud. In this case, ensure the following endpoints are accessible from co-managed devices:
>
> | Endpoint  | Function  |
> |-----------|-----------|
> | `https://*.events.data.microsoft.com` | Used by managed devices to send [required functional data](data-collection.md#data-collection) to the Intune data collection endpoint. |
>
>For more information and troubleshooting proxy configurations, see [Troubleshoot endpoint analytics](troubleshoot.md#proxy-server-authentication).
::: zone-end

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::
::: zone pivot="intune"

> Devices enrolled in endpoint analytics need a valid license for the use of Microsoft Intune. For more information, see [Microsoft Intune licensing](../intune-service/fundamentals/licenses.md).

::: zone-end

::: zone pivot="cm"

> Devices enrolled in endpoint analytics need a valid license for the use of Microsoft Intune. For more information, see [Microsoft Configuration Manager licensing](../configmgr/core/understand/learn-more-editions.md).

::: zone-end
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> Endpoint analytics includes tasks that require different levels of permissions.
>
> For a detailed breakdown of the required permissions for each task:
>
> - [RBAC requirements for configuring endpoint analytics](configure.md#prerequisites)
> - [RBAC requirements for rewieving endpoint analytics data](scores.md#prerequisites)
:::column-end:::
:::row-end:::

::: zone pivot="cm"

## Configuration Manager requirements

To use endpoint analytics, your environment must have [tenant attach](../configmgr/tenant-attach/device-sync-actions.md) enabled. Tenant attach connects Configuration Manager to Intune, allowing you to manage devices from the Intune admin center and perform actions such as device sync and remote tasks.

> [!NOTE]
> Using multiple Configuration Manager hierarchies with a single endpoint analytics instance isn't supported.

::: zone-end

## Reports available in endpoint analytics

Endpoint analytics organizes insights into reports that highlight performance and reliability issues across managed devices. Common examples include:

- Startup performance: Identifies devices with slow boot times and contributing factors.
- Application reliability: Tracks app crashes and stability trends.
- Restart frequency: Highlights devices that restart often, signaling potential hardware or software issues.

## Next Steps

Learn more about endpoint analytics:

- [Configure endpoint analytics](configure.md)
- [Scores, baselines, and insights](scores.md)
- Understand the reports:
  - [Startup performance](startup-performance.md)
  - [Restart frequency](restart-frequency.md)
  - [Application reliability](app-reliability.md)
  - [Work from anywhere](work-from-anywhere.md)
- [Understand data collection](data-collection.md)
- [Microsoft Intune Advanced Analytics](../advanced-analytics/index.md)
