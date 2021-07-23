---
# required metadata
title: Monitor Windows 365 devices
titleSuffix:
description: Learn how to monitor Windows 365 devices.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 07/26/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Monitor Windows 365 devices with Endpoint Analytics

Cloud PC monitoring in Endpoint Analytics provides granular insights and reports at the device level. IT admins can use these reports to assess performance, take actions, reduce help desk calls, and enhance productivity. Cloud PC has six reporting categories with metrics, tenant scores, and baselines along with actionable insights and recommendations such as device upgrades. Cloud PC score in Endpoint Analytics also helps improve Productivity Score.

All metrics and scores are at the device and user level to identify users that need support to improve performance.

The six reporting categories for Cloud PC are:

1. **Resource performance**: Performance slows down if CPU or RAM spike time % is consistently high. This report provides the following performance data:
    - CPU and RAM spike time %.
    - Thresholds.
    - Scores and recommendations on how to improve device performance (device upgrades).
    - Top 10 processes causing the end user experience to slow down.
2. **Remoting Connection**: Remoting metrics tell you how much time it takes a user to log in to a Cloud PC to access the full desktop and apps. This report includes the following data:
    - **Round Trip Time** for the users by location and CPC SKUs.
    - **Log-in failures** so admins can identify users getting impacted.
3. **Startup performance**: The startup performance score helps IT get users from power-on to productivity quickly, without lengthy boot and sign-in delays.
4. **Proactive Remediation**: Cloud PC remediation scripts help admins and organizations reduce CSS costs, support calls, or raise tickets. These are automated actions to remediate common issues or issues resulting in help desk calls. Admins can configure these PowerShell scripts, specify the type of script and various conditions under which it can execute, and also identify which groups of Cloud PC devices they apply to.
5. **Recommended software**: A list of recommended software that can improve the end-user experience, independent of lower-level health metrics.
6. **App health**: The number of Cloud PC devices running certain apps, crash date by each app type in the tenant, and scores and thresholds for optimal performance.

<!-- ########################## -->
## Next steps

[Resize a Cloud PC](resize-cloud-pc.md).
