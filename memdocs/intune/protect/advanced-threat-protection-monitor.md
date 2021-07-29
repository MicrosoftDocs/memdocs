---
# required metadata

title: Monitor integration of Microsoft Defender for Endpoint in Microsoft Intune
description: Monitor Microsoft Defender for Endpoint with Intune, including device compliance and onboarding status.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.reviewer: aanavath

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Monitor device status when you integrate Microsoft Defender for Endpoint with Intune

When you integrate Microsoft Intune and Microsoft Defender for Endpoint, you can view information about device compliance and onboarding in the Microsoft Endpoint Manager admin center.

## Monitor device compliance

Monitor the state of devices that have the Microsoft Defender for Endpoint compliance policy.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Monitor** > **Policy compliance**.

3. Find your Microsoft Defender for Endpoint policy in the list, and see which devices are compliant or noncompliant.

You can also use the *operational* report for noncompliant devices from the same location:

- Select **Devices** > **Monitor** > **Noncompliant devices**.

For more information about reports, see [Intune reports](../fundamentals/reports.md).

## View onboarding status

To view the onboarding status of your Intune-managed devices, go to **Endpoint security** > **Microsoft Defender for Endpoint**. From this page, you can also create a device configuration profile to onboard more devices to Microsoft Defender for Endpoint.

## Next steps

[Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md)
