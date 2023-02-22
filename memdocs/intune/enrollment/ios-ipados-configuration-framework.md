---
# required metadata

title: iOS/iPadOS security configuration framework
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings available for iOS/iPadOS device  security.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/15/2021
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

# iOS/iPadOS Enterprise security configuration framework

The iOS/iPadOS security configuration framework is a series of recommendations for device compliance and configuration policy settings. These recommendations help you tailor your organization's mobile device security protection to your specific needs.They include recommended device compliance and device restriction settings for basic, enhanced, and high security. 

This taxonomy is explained in the following articles:

- [iOS/iPadOS framework deployment methodology](ios-ipados-framework-deployment-methodology.md): A recommended methodology for deploying the security configuration framework.
-  [Set app configuration policies for iOS/iPadOS devices](ios-ipados-app-configuration-policies.md): Configure apps on the devices to disallow personal accounts.
- [iOS/iPadOS device compliance security settings](ios-ipados-device-compliance-security-configurations.md): Specific configuration settings for ensuring personally owned and corporate owned devices are healthy and compliant.
- [iOS/iPadOS personal device security settings](ios-ipados-personal-device-security-configurations.md): Specific configuration settings for basic, enhanced, and high security on personally owned devices.
- [iOS/iPadOS supervised device security settings](ios-ipados-supervised-device-security-configurations.md): Specific configuration settings for basic, enhanced, and high security on corporate owned supervised devices.

## iOS/iPadOS enrollment modes

iOS/iPadOS supports several enrollment scenarios, two of which are covered as part of this framework:

- [Device enrollment for personally owned devices](ios-enroll.md): These devices are personally owned and used for both work and personal use.
- [Supervised automated device enrollment for corporate-owned devices](device-enrollment-program-enroll-ios.md): These devices are corporate-owned, associated with a single user, and used exclusively for work and not personal use.  

## iOS/iPadOS framework deployment methodology

[!INCLUDE [framework methodology](../includes/framework-deployment-methodology.md)]

When testing changes to iOS/iPadOS devices, be aware of the [delivery timing](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned). The status of compliance policies for devices can be monitored. For more information, see [Monitor Intune device compliance policies](../protect/compliance-policy-monitor.md) and [Monitor device profiles in Microsoft Intune](../configuration/device-profile-monitor.md). 

## Next steps  

1. [Configure app configuration policies](ios-ipados-app-configuration-policies.md)
2. [Configure device compliance security policies](ios-ipados-device-compliance-security-configurations.md)
3. [Configure device security policies for personal devices](ios-ipados-personal-device-security-configurations.md)  
4. [Configure device security policies for supervised devices](ios-ipados-supervised-device-security-configurations.md) 

