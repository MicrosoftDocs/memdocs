---
title: Deploying Advanced Analytics
titleSuffix: Microsoft Intune
description: Learn how to deploy Advanced Analytics features
ms.date: 09/10/2025
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: concept-article
author: MandiOhlinger
ms.author: mandia
manager: laurawi
---

# Deploying Advanced Analytics

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

[!INCLUDE [advanced-analytics-overview](includes/advanced-analytics-overview.md)]

## Enabling Advanced Analytics in Microsoft Intune

When license requirements are met, then Advanced Analytics capabilities are automatically enabled in your tenant.

> [!NOTE]
> It may take up to 48 hours after you buy licenses or start a trial to see Advanced Analytics features in your tenant.

For the extra reports and capabilities on Windows devices:

1. Devices need to be enrolled into Intune and onboarded to Endpoint analytics and meet the [Prerequisites](advanced-analytics-plan.md#prerequisites):

    - [Onboard and enroll your Intune-managed devices to Endpoint analytics](enroll-intune.md)
    - [Onboard and enroll your co-managed devices to Endpoint analytics](enroll-configmgr.md)

1. For Multi Device query, a [properties catalog policy](/intune/intune-service/configuration/properties-catalog) needs to be configured and deployed.

## Integrating Advanced Analytics into your business

1. Update role based access control for custom roles to include new permissions such as **Managed Devices** > **Query** for [Device Query](device-query.md). For more information, see [Role-based access control](../intune-service/fundamentals/role-based-access-control.md)
1. Update support processes to:
    1. Use [device timeline](enhanced-device-timeline.md) to review if there's a specific pattern, such as a device restart or update tied to the anomaly.
    1. Use [device query](device-query.md) retrieve live information from a device to aid troubleshooting.

1. Implement processes to periodically review:
    1. [Anomaly Detection Data](anomaly-detection.md). For example, after application or operating system updates are applied to proactively identify issues.
    1. [Battery health data](battery-health.md) to identify devices that may need attention to ensure long battery life and good user experience.
    1. [Resource performance reports](resource-performance-report.md) to identify challenges with resource performance by device, model, and manufacturer to aid in future purchasing decisions.

---

## Next Steps

> [!div class="nextstepaction"]
> [Next: Learn about Anomaly Detection >](anomaly-detection.md)

---

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)
