---
title: Quickstart - Enroll Intune devices
titleSuffix: Microsoft Endpoint Manager
description: In this quickstart, you enroll Intune devices into Endpoint analytics.
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: quickstart
author: mestew
ms.author: mstewart
manager: dougeby
# Customer intent: As a Microsoft Endpoint Manager administrator, I want to enroll Intune devices into Endpoint analytics so that I can gain insights into the user experience.
ms.localizationpriority: high
ms.collection: highpri
---

# Quickstart: Enroll Intune devices into Endpoint analytics

This quickstart outlines prerequisites and instructions for enrolling Intune managed devices into Endpoint analytics. If your devices are co-managed and meet the [Intune device requirements](#bkmk_prereq) below, we recommend using the instructions in this quickstart to enroll them to Endpoint analytics via Intune. Note that you do not need to move any co-management workloads to Intune to enroll eligible devices via Intune.

## <a name="bkmk_prereq"></a> Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:  

### Intune device requirements

- Intune enrolled or co-managed devices running the following:
   - Windows 10 version 1903 or later
      - The cumulative update from July 2021 or later installed
     - Pro, Pro Education, Enterprise, or Education. Home and long-term servicing channel (LTSC) aren't supported.

- Windows devices must be Azure AD joined or hybrid Azure AD joined.
   - Workplace joined or Azure AD registered devices aren't supported.
- The **Connected User Experiences and Telemetry** service on the device is running

### <a name="bkmk_endpoints"></a> Endpoints required for Intune-managed devices

To enroll devices to Endpoint analytics, they need to send required functional data to Microsoft public cloud. Endpoint Analytics uses the Windows **Connected User Experiences and Telemetry** component (DiagTrack) to collect the data from Intune-managed devices.

| Endpoint  | Function  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Used by Intune-managed devices to send [required functional data](data-collection.md#bkmk_datacollection) to the Intune data collection endpoint. |

### Licensing Prerequisites

Devices enrolled in Endpoint analytics need a valid license for the use of Microsoft Endpoint Manager. For more information, see [Microsoft Intune licensing](../intune/fundamentals/licenses.md) or [Microsoft Endpoint Configuration Manager licensing](../configmgr/core/understand/learn-more-editions.md).

### Endpoint analytics permissions

- The [Intune Service Administrator role](../intune/fundamentals/role-based-access-control.md) is required to [start gathering data](#bkmk_onboard).
   - After clicking **Start** for gathering data, other read-only roles can view the data.

[!INCLUDE [Endpoint analytics permissions information](includes/endpoint-analytics-rbac.md)]

## <a name="bkmk_onboard"></a> Onboard in the Endpoint analytics portal
Onboarding from  the Endpoint analytics portal is required for Intune managed devices. For more information about common issues, see [Troubleshooting device enrollment and startup performance](troubleshoot.md#bkmk_enrollment_tshooter).

[!INCLUDE [Endpoint analytics overview page information](includes/onboard.md)]

## <a name="bkmk_view"></a> View the Overview page

You won't see your data immediately. The data needs to be gathered and the results calculated. For startup performance, the device needs to have been restarted at least once. Once your data is ready, you'll notice some information on the **Overview** page, explained in more detail below:

[!INCLUDE [Endpoint analytics overview page information](includes/overview-page.md)]

## Next steps

[Enroll Configuration Manager devices](enroll-configmgr.md)
