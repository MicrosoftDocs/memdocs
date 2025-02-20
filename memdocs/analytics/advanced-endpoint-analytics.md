---
title: What is Microsoft Intune Advanced Analytics
titleSuffix: Microsoft Intune
description: Learn about Intune Advanced Analytics
ms.date: 08/01/2024
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: conceptual
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---

# What is Microsoft Intune Advanced Analytics

> [!NOTE]
> This capability is available as an Intune add-on. For more information, see [Intune add-ons](../intune-service/fundamentals/intune-add-ons.md).

Microsoft Intune Advanced Analytics provides comprehensive visibility of the end-user experience in your organization and optimizes it with data driven insights. With Intune Advanced Analytics, your organization can proactively detect and resolve endpoint issues, streamline troubleshooting process, and improve your users' technology experience.

The Microsoft Intune Suite includes features for Advanced Analytics, such as:

- **Custom device scopes** allow you to use [Scope tags](../intune-service/fundamentals/scope-tags.md) to slice Endpoint analytics reports to a subset of devices. You can see scores, insights, and recommendations specific to subsets of your enrolled devices. For example,  you can focus on devices that you manage, devices assigned to a specific business group, or devices located in a particular geographic region. For more information, see [Device scopes](device-scopes.md).

- **Anomalies** monitors the health of devices in your organization for user experience and productivity regressions following configuration changes. For more information, see [Anomaly detection](anomaly-detection.md).

- An **Enhanced device timeline** includes more events and lower data latency to assist with troubleshooting device issues. For more information, see [Enhanced device timeline](enhanced-device-timeline.md).

- **Device query** enables you to get near-real time access to data about the state and configuration of devices. For more information, see [Device query](device-query.md).

- A **Battery health** report to gain visibility into hardware performance issues impacting user technology experience. For more information, see [Battery health](battery-health.md)

Intune Advanced Analytics is automatically integrated into the existing base Endpoint analytics experience in the Intune admin center under **Reports** > **Endpoint analytics**.

## Prerequisites

Intune Advanced Analytics features build on top of the existing base Endpoint analytics experience. You must [onboard and enroll your Intune-managed devices to Endpoint analytics](enroll-intune.md) to use the advanced features.

> [!NOTE]
> The Advanced Analytics features are only available for Intune-managed (including co-managed) devices.

## License requirements

In addition to [license requirements](enroll-intune.md#licensing-prerequisites) for Endpoint analytics, an add-on license is required to use features in Intune Advanced Analytics.

The Advanced Analytics features are included under [Microsoft Intune Suite](../intune-service/fundamentals/intune-add-ons.md) and requires an extra cost to the licensing options that include Microsoft Intune. The capabilities are also available as an individual add-on to Microsoft subscriptions that include Intune. Global and billing administrators can use the centralized experience (Intune add-ons) in the Intune admin center to easily access trial licenses (up to 250 users for 90 days) and licenses to purchase.

## Government cloud support

Advanced Endpoint Analytics is supported with the following sovereign cloud environments:

- U.S. Government Community Cloud (GCC) High
- U.S. Department of Defense (DoD)

> [!NOTE]
>
> Support for Advanced Endpoint Analytics in GCC High and DoD environments does not include the [*Device query*](device-query.md) functionality.

For more information, see [Microsoft Intune for US Government GCC service description](../intune-service/fundamentals/intune-govt-service-description.md).

## Mixed licensing scenarios

When some users in your tenant have access to Advanced Analytics through an add-on subscription or trial, while others only have access to the base Endpoint analytics product, it's called a mixed license scenario.

Currently, the highest functional subscription sets the Endpoint analytics experience for your tenant. In the earlier example, your tenant experience would include advanced features in Endpoint analytics for all enrolled devices.  

## Enabling Advanced Analytics in Microsoft Intune

When license requirements are met, then Advanced Analytics features are automatically enabled in your tenant. If licenses expire or you change your subscription to one that doesn't include Advanced Analytics, your tenant is automatically reverted to the base Endpoint analytics experience.

> [!NOTE]
> It may take up to 48 hours after you buy licenses or start a trial to see Advanced Analytics features in your tenant.

## Next Steps

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)  
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)