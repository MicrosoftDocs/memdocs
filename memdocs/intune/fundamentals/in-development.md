---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 09/21/2022
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

## Device management

###  Support for Locate device on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices<!-- 12391424 -->
You'll be able to use "Locate device" on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices. Using this feature, admins will be able to locate lost or stolen corporate devices on-demand. To do this, in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices**, and then select **All devices**. From the list of devices you manage, select a supported device, and choose the **Locate device** remote action.

For information on locating lost or stolen devices with Intune, go to:
 - [Locate lost or stolen devices with Intune](../remote-actions/device-locate.md)

Applies to:
- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

<!-- ***********************************************-->

## Device enrollment

### Windows Autopilot diagnostics will capture ESP failures<!-- 1895390 -->
Windows Autopilot diagnostics will automatically capture diagnostics about Windows Autopilot failures that occur on the Enrollment Status Page (ESP). Diagnostics will be available to download in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  

<!-- ***********************************************-->

## Device configuration

### Filter app and group policy assignments using Windows 11 SE operating system SKUs<!-- 10588651 -->
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

Two new Windows 11 SE operating system SKU's will added. You'll be able to use these SKUs in your assignment filters to include or exclude Windows 11 SE devices from applying group-targeted policies and applications.

For more information on filters and the device properties you can currently use, go to:
- [Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md)
- [Device properties, operators, and rule editing when creating filters in Microsoft Endpoint Manager](filters-device-properties.md)

Applies to:
- Windows 11 SE

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

## Device security

### Reusable groups of settings for Microsoft Defender Firewall Rules<!-- 5653346, 6009541 -->
 You’ll soon be able to add reusable groups of settings to your profiles for Microsoft Defender Firewall Rules. The reusable groups are collections of remote IP addresses and FQDNs that you define one time and can then use with one or more firewall rule profiles. You’ll no longer need to reconfigure the same group of IP addresses in each individual profile that might require them.  

Features of the reusable settings groups will include:  
- Add one or more remote IP addresses.  
- Add one or more FQDNs that can auto resolve to the remote IP address, or for one or more simple keywords when auto resolve for the group is off.  
- Use each settings group with one or more firewall rule profiles and the different  profiles can support different access configurations for the group.  

  For example, you can create two firewall rule profiles that reference the same reusable settings group and assign each profile to a different group of devices. The first profile can block access to all the remote IP addresses in the reusable settings group, while the second profile can be configured to allow access.  

- Edits to a settings group that's in use are automatically applied to the Firewall Rules profiles that use that group.  
  
Reusable groups will be configured on a new Tab for *Reusable settings* that will be available when you view endpoint security Firewall policy.  In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Firewall**.

<!-- ***********************************************-->

## Monitor and troubleshoot

### Open Help and Support without losing your context in the Microsoft Endpoint Manager admin center<!-- 12469338 -->
You’ll soon be able to use the **?** icon in the Microsoft Endpoint Manager admin center to  open a help and support session without losing your current node of focus in the admin center. The **?** icon is always available in the upper right of the admin center title bar. This change will add an additional method for accessing *Help and support*.

When you select  **?**, the admin center will open a new and separate side-by-side pane you use to navigate the support experience. By opening this separate pane, you’ll be free to navigate the support experience without affecting your original location and focus on the admin center. You will however be free to navigate through the admin center in that original pane if you choose.

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
