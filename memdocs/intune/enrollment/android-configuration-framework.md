---
# required metadata

title: Android Enterprise security configuration framework
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings available for Android Enterprise device basic and high security.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Android Enterprise security configuration framework

The Android Enterprise security configuration framework is a series of recommendations for device compliance and configuration policy settings. These recommendations help you tailor your organization's mobile device security protection to your specific needs, and include: 

* Device enrollment restrictions for personally owned work profile. 
* App configuration policies for fully managed devices.  
* Basic and high-level security settings for personally owned work profile. 
* Basic, enhanced, and high-level security settings for fully managed devices. 

The security framework provides recommendations for the following Android Enterprise management solutions:

- Fully managed: Corporate-owned devices, associated with a single user, used exclusively for work and not personal use.  
- Personally-owned work profile and corporate-owned work profile: User-owned devices, for BYOD scenarios, creates clear boundary between work and personal data on device.  

## Deployment methodology  

[!INCLUDE [framework methodology](../includes/framework-deployment-methodology.md)]

When testing changes to Android Enterprise devices, be aware of the [delivery timing](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals). The status of compliance policies for devices can be monitored. For more information, see [Monitor Intune device compliance policies](../protect/compliance-policy-monitor.md) and [Monitor device profiles in Microsoft Intune](../configuration/device-profile-monitor.md). 


## Next steps

1. [Configure device enrollment restrictions for personal devices](device-enrollment-restrictions.md)
2. [Configure app configuration policies](android-app-configuration-policies.md)
3. [Configure security settings for personal devices](android-work-profile-security-settings.md)  
4. [Configure security settings for fully managed devices](android-fully-managed-security-settings.md)  