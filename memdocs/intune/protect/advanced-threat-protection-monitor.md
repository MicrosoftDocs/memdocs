---
# required metadata

title: Monitor Microsoft Defender for Endpoint with Microsoft Intune
description: Monitor Microsoft Defender for Endpoint with Intune, including device compliance and onboarding status.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 10/10/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.reviewer: aanavath

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
---

# Monitor device status when you integrate Microsoft Defender for Endpoint with Intune

When you integrate Microsoft Intune and Microsoft Defender for Endpoint, you can view information about device compliance and onboarding in the Microsoft Intune admin center.

## Monitor device compliance

Monitor the state of devices that have the Microsoft Defender for Endpoint compliance policy.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance**. On the **Monitor** tab, select **Noncompliant devices**.

3. Find your Microsoft Defender for Endpoint policy in the list, and see which devices are compliant or noncompliant.

For more information about reports, see [Intune reports](../fundamentals/reports.md).

## View onboarding status

To view the onboarding status of your Intune-managed devices:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Overview**. As part of the default *Summary* is a visualization report for **Windows devices onboarded onto Microsoft Defender for Endpoint**, which displays the count of devices that report status from the Defender for Endpoint sensor.

## Related content

[Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md)
