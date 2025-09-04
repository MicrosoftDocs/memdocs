---
title: Planning for Advanced Analytics
titleSuffix: Microsoft Intune
description: Learn about the requirements and fundamentals of Intune Advanced Analytics
ms.date: 08/01/2024
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: concept-article
author: MandiOhlinger
ms.author: mandia
manager: laurawi
ms.localizationpriority: high
---

# Plan for Advanced Analytics

[!INCLUDE [intune-add-on-note](/intune/intune-service/includes/intune-add-on-note.md)]

[!INCLUDE [advanced-analytics-overview](/intune/analytics/includes/advanced-analytics-overview.md)]

## Planning Checklist

For a successful deployment of Advanced Analytics, the following activities are recommended:

- Review licensing and enable required features in your Microsoft 365 tenant
- Identify target device groups for analytics rollout
- Assess your organization's privacy and compliance requirements for device data. Review the Intune data platform schema to understand the full list of data captured
- Communicate planned changes and benefits to stakeholders and end users
- Ensure the right stakeholders from IT functions are part of the implementation project, to allow realisation of the benefits through IT process optimization.
- Establish escalation and support procedures for analytics findings
- Define reporting and monitoring objectives (e.g., proactive device health, security anomaly tracking)
- Review and train staff on IT processes you aim to optimise with the implementation of Advanced Analytics (1st line ticket triage, hardware refresh cycles, app update processes, etc). Think of this as a continuous improvement cycle, with faster issue resolution and proactive issue resolution.

## Prerequisites

Intune Advanced Analytics features build on top of the existing base Endpoint analytics experience.

> [!NOTE]
> The Advanced Analytics features are only available for Intune-managed (including co-managed) devices.

General requirements:

- Advanced Analytics features are included under [Microsoft Intune Suite](../intune-service/fundamentals/intune-add-ons.md) and requires an extra cost to the licensing options that include Microsoft Intune. The capabilities are also available as an individual add-on to Microsoft subscriptions that include Intune.
- Network connectivity to required Microsoft endpoints
 For iOS/iPadOS, Android, and macOS, data is automatically collected and a separate properties catalog policy does not need to be deployed.

Windows capability requirements:

- Windows 10/11 (minimum build 1903 or later recommended).
- Microsoft Entra-joined or Hybrid Entra-joined.
- [Endpoint analytics for Windows license requirements](enroll-intune.md#licensing-prerequisites).
- Device enrolled into Intune and onboarded to Endpoint analytics
  - [Onboard and enroll your Intune-managed devices to Endpoint analytics](enroll-intune.md)
  - [Onboard and enroll your co-managed devices to Endpoint analytics](enroll-configmgr.md)
- Multi Device query requires a [properties catalog policy](/intune/intune-service/configuration/properties-catalog) to be configured and deployed.
- Single device query requires the device to be marked as corporate.

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

---

## Next Steps

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)  
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)
