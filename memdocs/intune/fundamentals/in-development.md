---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 10/24/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: 
  - M365-identity-device-management
  - highpri
  - highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. In addition to the information in this article:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control

-->

<!-- ***********************************************-->

## App management

### Global quiet time app policy settings<!-- 15424417 -->
The global quiet time settings will allow you to create policies to schedule quiet time for your end users which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you will be able to find it in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

## Device management

### Endpoint security firewall rules support for ICMP type<!-- 5653356 -->
We’re adding a new setting named **IcmpTypesAndCodes** to the endpoint security firewall rules template for Windows 10. To configure this in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Firewall** > **Create Policy** > Platform: *Windows 10, Windows 11, and Windows Server*  > Profile: *Microsoft Defender Firewall Rules*).

With this new setting you’ll be able to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule.

Applies to:  
- Windows 10, Windows 11, and Windows Server

<!-- ***********************************************-->

## Device enrollment

### Windows Autopilot diagnostics will capture ESP failures<!-- 1895390 -->
Windows Autopilot diagnostics will automatically capture diagnostics about Windows Autopilot failures that occur on the Enrollment Status Page (ESP). Diagnostics will be available to download in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  

<!-- ***********************************************-->

## Device configuration

### New password complexity requirements for Android Enterprise 12+ personally owned devices with a work profile<!-- 12436068 -->
On Android Enterprise 11 and older personally owned devices with a work profile, you can set the **Required password type** and a **Minimum password length** in device configuration profiles and compliance policies.

Google is deprecating these features for Android 12+ personally owned devices with a work profile and replacing them with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).

The new **Password complexity** setting will have the following options:

- **Not configured**: Intune doesn't change or update this setting. By default, the OS may not require a password.
- **Low**: Pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.
- **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least 4 characters.
- **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters.

If you currently use the **Required password type** and **Minimum password length** settings in your device configuration and compliance policies on Android 12+, then we recommend using the new **Password complexity** setting instead.

If you continue to use the **Required password type** and **Minimum password length** settings, and don't configure the **Password complexity** setting, then new devices running Android 12+ will default to the **High** password complexity.

There is no impact for existing devices with the **Required password type** and **Minimum password length** settings configured.

For more information on the existing settings you can configure, go to:

- [Android Enterprise personally owned devices with a work profile - configuration profile settings list](../configuration/device-restrictions-android-for-work.md#personally-owned-devices-with-a-work-profile)
- [Android Enterprise personally owned devices with a work profile - compliance policy settings list](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)

Applies to:
- Android 12.0 and newer
- Android Enterprise personally owned devices with a work profile


<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
