---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 09/20/2023
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
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Tenant administration
## Notices
-->

<!-- ***********************************************-->

## App management  

### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The "SafetyNet device attestation" setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### Advanced application management<!-- 10986080  -->  
Advanced application management provides you with an enterprise catalog of applications that are easily accessible. It also provides application update capabilities. The enterprise catalog is planned to be available in public preview in late Q2 2023. The application update capabilities are planned to be available in early Q3 2023.

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Support for multi-SIM iOS/iPadOS device inventory<!--17016690 (replaced 16360290 for tracking -->  
You'll be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:

- **ICCID**
- **IMEI**
- **MEID**
- **Phone number**

These fields will default to using labels returned by the device, such as:  *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:

- **iOS/iPadOS**

<!-- *********************************************** -->

<!-- ## Device configuration -->
 
<!-- *********************************************** -->

<!-- ## Device enrollment  -->

<!-- *********************************************** -->

## Device management

### Introducing Remote Help on macOS <!-- 12454029 -->

The Remote Help web app allows users to connect to macOS devices and join a view-only remote assistance session.

For more information on Remote Help, go to [Remote Help](../fundamentals/remote-help.md).

Applies to:

- Safari 16.4+
- macOS 11 Big Sur

### Government tenant support for endpoint security Application Control policy and Managed Installer<!-- 24850055 -->
We're adding support to use endpoint security Application Control policies, and to configure a Managed Installer, to both tenants in US Government and tenants in 21Vianet in China.

Support for Application Control policy and Managed installers was originally [released in preview in June 2023](../fundamentals/whats-new.md#new-endpoint-security-application-control-policy-in-preview) as part of the Intune 2306 service release. Application Control policies in Intune are an implementation of Defender Application Control (WDAC).


<!-- *********************************************** -->

## Device security

### Linux support with Intune Endpoint security policies for Endpoint detection and response<!--  17757972 -->  
Intune Endpoint security policies for *Endpoint detection  and response* (EDR) will soon support Linux.  We're adding a new profile template that you can use with both the Linux devices enrolled with Intune and macOS devices managed through the opt-in public preview of the  [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) scenario.

The Linux EDR template will include the following settings for the Device tags category from Defender for Endpoint:
- **Group tag**  – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn't be repeated in the same profile.

You can learn more about Defender for Endpoint settings that are available for Linux in [Set preferences for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-preferences#device-tags) in the Defender documentation.

<!-- *********************************************** -->

<!-- ## Monitor and troubleshoot -->

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
