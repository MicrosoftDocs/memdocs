---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 08/24/2023
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

## Device configuration

#### Config Refresh will be in the Settings Catalog for Windows Insiders<!-- 15060174 -->
In the Windows Settings Catalog, you can configure Config Refresh. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check-in to Intune.

For more information on the Settings Catalog, go to [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

Applies to:
- Windows 10 and later

### Managed Settings now available in the Apple settings catalog <!-- 21083384 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

The settings within the Managed Settings command are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** > **Settings catalog** for profile type.

**Managed Settings > App Analytics**:
- Enabled: If true, enable sharing app analytics with app developers. If false, disable sharing app analytics.

Applies to:
- Shared iPad

**Managed Settings > Accessibility Settings**:
- Bold Text Enabled
- Grayscale Enabled
- Increase Contrast Enabled
- Reduce Motion Enabled
- Reduce Transparency Enabled
- Text Size
- Touch Accommodations Enabled
- Voice Over Enabled
- Zoom Enabled

**Managed Settings > Personal Hotspot**:
- Enabled: If true, enable Personal Hotspot. If false, disable Personal Hotspot.

**Managed Settings > Software Update Settings**:
- Recommendation Cadence: This value defines how the system presents software updates to the user.

**Managed Settings > Time Zone**:
- Time Zone: The Internet Assigned Numbers Authority (IANA) time zone database name.

Applies to:
- iOS/iPadOS

**Managed Settings > Bluetooth**:
- Enabled: If true, enable the Bluetooth setting. If false, disable the Bluetooth setting.

**Managed Settings > MDM Options**:
- Activation Lock Allowed While Supervised: If true, a supervised device registers itself with Activation Lock when the user enables Find My.

Applies to:
- iOS/iPadOS
- macOS

For more information on these settings, go to [Apple's developer website](https://developer.apple.com/documentation/devicemanagement/settingscommand/command/settings). For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### New setting available in the macOS settings catalog<!-- 24809885 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There is a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration profiles** > **Create profile** > **macOS** > **Settings catalog** for profile type.  

**Microsoft Defender > Cloud delivered protection preferences**:
- Cloud Block Level

Applies to:
- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).


<!-- *********************************************** -->

## Device enrollment

### SSO support for fully managed and corporate-owned devices with a work profile<!-- 8080357 --> 
Intune will support single sign-on (SSO) on Android Enterprise devices that are fully managed or corporate-owned with a work profile.  With the addition of SSO, people enrolling their devices will only need to sign in once with their work or school account during enrollment.

<!-- *********************************************** -->

## Device management

### Introducing Remote Help on macOS <!-- 12454029 -->

The Remote Help web app allows users to connect to macOS devices and join a view-only remote assistance session.

For more information on Remote Help, go to [Remote Help](../fundamentals/remote-help.md).

Applies to: 
- Safari 16.4+
- macOS 11 Big Sur

### Government tenant support for endpoint security Application Control policy and Managed Installer<!-- 24850055 -->
We’re adding support to use endpoint security Application Control policies, and to configure a Managed Installer, to both tenants in US Government and tenants in 21Vianet in China.

Support for Application Control policy and Managed installers was originally [released in preview in June 2023](../fundamentals/whats-new.md#new-endpoint-security-application-control-policy-in-preview) as part of the Intune 2306 service release. Application Control policies in Intune are an implementation of Defender Application Control (WDAC).

### Management certificate expiration date<!-- 17648747 -->
Management certificate expiration date will be available as a column in the **Devices** workload. You will be able to filter on a range of expiration dates for the management certificate and also export a list of devices with an expiration date matching the filter. You will find this information listed in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **All devices**.

### Intune will support iOS/iPadOS 15.x as the minimum version<!-- 24161619  -->  
Later this year, Apple is expected to release iOS/iPadOS version 17. After the release of iOS/iPadOS 17, the minimum version supported by Intune will be iOS/iPadOS 15.x.

For more information on this change, go to [Plan for change: Intune is moving to support iOS/iPadOS 15 and later](whats-new.md#plan-for-change-intune-is-moving-to-support-iosipados-15-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, go to [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device security

### Endpoint Privilege Management support for Windows 365 devices<!-- 17016794 -->
We are adding support to manage application elevations on Windows 365 devices (also known as Cloud PCs) to [Endpoint Privilege Management](../protect/epm-overview.md).  

### Linux support with Intune Endpoint security policies for Endpoint detection and response<!--  17757972 -->  
Intune Endpoint security policies for *Endpoint detection  and response* (EDR) will soon support Linux.  We’re adding a new profile template that you can use with both the Linux devices enrolled with Intune and macOS devices managed through the opt-in public preview of the  [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) scenario.

The Linux EDR template will include the following settings for the Device tags category from Defender for Endpoint:
- **Group tag**  – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn’t be repeated in the same profile.

You can learn more about Defender for Endpoint settings that are available for Linux in [Set preferences for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-preferences#device-tags) in the Defender documentation.

### macOS support with Intune Endpoint security policies for Endpoint detection and response<!--  17757981 -->  
Intune Endpoint security policies for *Endpoint detection  and response* (EDR) will soon support macOS.  We’re adding a new profile template that you can use with both the macOS devices enrolled with Intune and macOS devices managed through the opt-in public preview of the  [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) scenario.

The macOS EDR template will include the following settings for the Device tags category from Defender for Endpoint:
- **Type of  tag**  – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn’t be repeated in the same profile.

You can learn more about Defender for Endpoint settings that are available for macOS in  [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences#device-tags) in the Defender documentation.


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
