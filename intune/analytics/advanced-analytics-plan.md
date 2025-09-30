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

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

[!INCLUDE [advanced-analytics-overview](includes/advanced-analytics-overview.md)]

For a successful deployment of Advanced Analytics, the following activities are recommended:

- Assess your organization's privacy and compliance requirements for device data. Review the Intune [data platform schema](data-platform-schema.md) to understand the full list of data captured.
- Establish escalation and support procedures for analytics findings.
- Review and train staff on IT processes you aim to optimize with the implementation of Advanced Analytics. Examples include help desk triage, hardware refresh cycles and application updates. Think of this as a continuous improvement cycle, with faster issue resolution and proactive issue resolution.

## Prerequisites

Intune Advanced Analytics features build on top of the base Endpoint analytics experience.

> [!NOTE]
> The Advanced Analytics features are only available for Intune-managed (including co-managed) devices.

General requirements:

- Advanced Analytics features are included in [Microsoft Intune Suite](../intune-service/fundamentals/intune-add-ons.md). The capabilities are also available as an individual add-on to Microsoft subscriptions that include Intune.
- Network connectivity to required Microsoft endpoints. For more information, see [Microsoft Intune URLs and IP address ranges](/mem/intune/fundamentals/intune-endpoints).

Windows capability requirements:

- Windows 10/11 (minimum build 1903 or later recommended).
- Microsoft Entra-joined or Hybrid Entra-joined.
- [Endpoint analytics for Windows license requirements](enroll-intune.md#licensing-prerequisites).
- Device enrolled into Intune and onboarded to Endpoint analytics
  - [Onboard and enroll your Intune-managed devices to Endpoint analytics](enroll-intune.md)
  - [Onboard and enroll your co-managed devices to Endpoint analytics](enroll-configmgr.md)
- Multi Device query requires a [properties catalog policy](/intune/intune-service/configuration/properties-catalog) to be configured and deployed.
- Single device query requires the device to be marked as corporate.
- Anamoly detection:
  - After enrollment, client devices require a restart to fully enable all analytics. <!--7698085-->
  - Devices enrolled from Configuration Manager need client version 2006, or later installed

> [!NOTE]
> For iOS/iPadOS, Android, and macOS, data is automatically collected and a separate properties catalog policy doesn't need to be deployed.

Device query for multiple devices is supported on devices running:  

- Windows 10 and later  
- Android  
  - Android Enterprise corporate owned dedicated devices (COSU)  
  - Android Enterprise corporate owned fully managed (COBO)  
  - Android Enterprise corporate owned work profile (COPE)  
- Apple  
  - iOS/iPadOS  
  - macOS  

## Government cloud support

Advanced Endpoint Analytics is supported with the following sovereign cloud environments:

- U.S. Government Community Cloud (GCC) High
- U.S. Department of Defense (DoD)

> [!NOTE]
>
> Support for Advanced Endpoint Analytics in GCC High and DoD environments doesn't include the [*Device query*](device-query.md) or [*Resource performance*](resource-performance-report.md) functionality.

For more information, see [Microsoft Intune for US Government GCC service description](../intune-service/fundamentals/intune-govt-service-description.md).

## Mixed licensing scenarios

A mixed licenisng scenario occurs when some users in your tenant have access to Advanced Analytics through an add-on subscription or trial, while others only have access to the base Endpoint analytics product.

Currently, the highest functional subscription sets the Endpoint analytics experience for your tenant. In the earlier example, your tenant experience would include advanced features in Endpoint analytics for all enrolled devices.

## Role based access control

- Anomaly detection uses built-in [role permissions](overview.md#built-in-role-permissions)
- For a user to use Device query, you must assign the Managed Devices > Query and Organization > Read permissions to them.

---

## Next Steps

> [!div class="nextstepaction"]
> [Next: Deploy Advanced Analytics >](advanced-analytics-deploy.md)

---

For more information, go to:

- [Anomaly detection](anomaly-detection.md)
- [Device scopes](device-scopes.md)
- [Enhanced device timeline](enhanced-device-timeline.md)  
- [Battery health](battery-health.md)
- [Device query](device-query.md)
- [Resource Performance report](resource-performance-report.md)
