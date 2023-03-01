---
title: What is advanced Endpoint analytics
titleSuffix: Microsoft Endpoint Manager
description: Learn about advanced features in Endpoint analytics
ms.date: 02/22/2023
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---

# What is advanced Endpoint analytics

> [!NOTE]
> This capability is available as an Intune add-on. For more information, see [Intune add-ons](../intune/fundamentals/intune-add-ons.md).

The Microsoft Intune Suite includes advanced features for Endpoint analytics, such as:

- **Custom device scopes** allow you to use [Scope tags](../intune/fundamentals/scope-tags.md) to slice Endpoint analytics reports to a subset of devices. You can see scores, insights, and recommendations specific to subsets of your enrolled devices, such as devices you're responsible to manage, or devices belonging to a particular business group or assigned to a specific geographic region. For more information, see [Device scopes](device-scopes.md).

- **Anomalies** monitors the health of devices in your organization for user experience and productivity regressions following configuration changes. For more information, see [Anomaly detection](anomaly-detection.md).

- An **enhanced device timeline** includes more events and lower data latency to assist with troubleshooting device issues. For more information, see [Enhanced device timeline](enhanced-device-timeline.md).

The advanced features in Endpoint analytics are automatically integrated into the existing base Endpoint analytics experience in the Intune admin center under **Reports** > **Endpoint analytics**.

## Prerequisites
 
The advanced features in Endpoint analytics build on top of the existing base Endpoint analytics experience. You must [onboard and enroll your Intune-managed devices to Endpoint analytics](enroll-intune.md) to use the advanced features.

> [!NOTE]
> The advanced features in Endpoint analytics are only available for Intune-managed (including co-managed) devices.

## License requirements

In addition to [license requirements](enroll-intune.md#licensing-prerequisites) for Endpoint analytics, an add-on license is required to use advanced features in Endpoint analytics. 

The advanced features in Endpoint analytics are included as an Intune-add on under [Microsoft Intune Suite](../intune/fundamentals/intune-add-ons.md) and requires an extra cost to the licensing options that include Microsoft Endpoint Manager or Intune.

## Mixed licensing scenarios

If your tenant has an Intune subscription that includes the base Endpoint analytics product for all users and an add-on subscription that contains advanced features in Endpoint analytics for a subset of users, it's considered a mixed license scenario.

Currently, the highest functional subscription sets the Endpoint aAnalytics experience for your tenant. In the earlier example, your tenant experience would include advanced features in Endpoint Analytics for all enrolled devices.  

## Enabling advanced features for Endpoint analytics 

When license requirements are met, then advanced features in Endpoint analytics are automatically enabled in your tenant. If licenses expire or you change your subscription to one that doesn't include advanced features in Endpoint analytics, your tenant will automatically revert to the base Endpoint analytics experience.  

> [!NOTE]
> It may take up to 48 hours after you buy licenses or start a trial to see advanced features in Endpoint analytics in your tenant. 

## Next Steps

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)  

