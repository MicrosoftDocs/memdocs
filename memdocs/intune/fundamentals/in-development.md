---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 10/31/2023
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

### New grace period status added in apps for Android, Android AOSP <!-- 13498172 13498291 -->  
The Intune Company Portal app for Android and Microsoft Intune app for Android AOSP will show a grace period status for devices that don't meet compliance requirements but are still within their given grace period.  Users will be able to see the date by which devices must be compliant, as well as the instructions for how to become compliant. If users don't update their device by the given date, the device will be marked as noncompliant.  

### Minimum version update for iOS Company Portal<!-- 17964541  -->  
Users will be required to update to v5.2311.1 of the iOS Company Portal. If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you'll likely need to push an update to the related devices that use this setting. Otherwise, no action is needed. If you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version will be prompted to update to the latest Company Portal app.

### Intune APP SDK for .NET MAUI<!-- 17696301   -->  
Using the Intune APP SDK for .NET MAUI, you'll be able to develop Android or iOS apps for Intune that incorporate the [.NET Multi-platform App UI](https://dotnet.microsoft.com/apps/maui). Apps developed using this framework will allow you to enforce [Intune mobile application management](../apps/app-management.md).

### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The "SafetyNet device attestation" setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### Enterprise application management<!-- 10986080  -->  
Enterprise Application Management provides a catalog of prepackaged applications designed to simplify discovery, delivery, and updates for third and first party apps. Enterprise Application Management will be generally available in early Q1 2024.

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Support for multi-SIM iOS/iPadOS device inventory<!--17016690 (replaced 16360290 for tracking) -->  
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

### The macOS Company Portal app will support platform SSO (public preview)<!-- 24325427  -->  
In Intune, you can configure the Enterprise single sign-on (SSO) plug-in on Apple devices using a device configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Templates > Device features** for profile > **Single sign-on app extension**).

The Company Portal app version will support the platform SSO settings for macOS 13 and later. Platform SSO allows you to sync your Microsoft Entra ID password to local accounts on Macs using the Enterprise Single Sign-On extension.

For more information on the Enterprise SSO plug-in, go to:

- [Use Intune to deploy the Microsoft Enterprise SSO plug-in for Apple devices](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)
- [Entra ID and the Microsoft Enterprise SSO plug-in overview for Apple devices](/azure/active-directory/develop/apple-sso-plugin)

Applies to:

- macOS 13 and later

### New settings available in the Apple settings catalog<!-- 25189345  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** > **Settings catalog** for profile type.

**Managed Settings**:

- Data roaming
- Personal hotspot
- Voice roaming (deprecated): This setting was deprecated in iOS 16.0 and replaced by Data roaming.

Applies to:

- iOS/iPadOS

**Managed Settings**:

- Diagnostic submission

Applies to:

- Shared iPad

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Use assignment filters on Endpoint Privilege Management (EPM) policies<!-- 25230705   -->  
You can use assignment filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy, like targeting devices with a specific OS version or a specific manufacturer.

You can use filters on Endpoint Privilege Management (EPM) policies.

For more information about assignment filters, go to [Use filters when assigning your apps, policies, and profiles in Intune](filters.md).

Applies to:

- Windows 10/11

<!-- *********************************************** -->

## Device enrollment

### Enrollment for iOS/iPadOS devices in Azure AD shared device mode moving to general availability<!-- 25199565 -->  
An Intune enrollment method that lets you enroll iOS/iPadOS devices in Azure AD shared device mode is moving out of public preview. This enrollment method is part of Apple automated device enrollment and available to configure in the Microsoft Intune admin center. Shared device mode enables your frontline workers to share a single device throughout the day, signing in and out as needed.

<!-- *********************************************** -->

## Device management

### Improvements to new device experience in admin center (public preview)<!-- 24155098, 25103808, 17705028 IDdraft idready -->
The following changes are coming to the new Devices experience and will be available to try in public preview in the Microsoft Intune admin center:   
- Additional entry points to platform-specific options: Access the platform pages from the **Devices** navigation menu.   
- Quick entry to monitoring reports: Select the titles of the metrics cards to go to the corresponding monitoring report.  
- Improved navigation menu: We added icons back in to provide more color and context as you navigate.  
Flip the toggle in the Microsoft Intune admin center to try out the new experience while it's in public preview and share your feedback. For more information, see [Try new Devices experience](microsoft-intune-admin-center-devices.md).  

### Introducing a remote action to pause the config refresh enforcement interval<!--24249019  -->  
In the Windows Settings Catalog you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check-in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action will be added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings will be enforced again.

The remote action **Pause config refresh** can be accessed from the device summary page.

For information on currently available Remote actions, see [Remote actions](../remote-actions/device-management.md).

<!-- *********************************************** -->

## Device security


### Additional settings for the Linux Antivirus policy template<!-- 24191424  -->  
We’re expanding support for Linux by adding the following settings to the *Microsoft Defender Antivirus* template for Linux devices:

- cloudblocklevel
- scanarhives
- scanafterdefinitionupdate
- maximumondemandscanthreads
- behaviormonitoring
- enablefilehashcomputation
- networkprotection
- enforcementlevel
- nonexecmountpolicy
- unmonitoredfilesystems

The Microsoft Defender Antivirus template for Linux is supported for devices managed by Intune, as well as those managed only by Defender through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview#linux) scenario when you use the opt-in public preview.

### Updated security baseline for Microsoft 365 Apps for Enterprise<!-- 25021846  -->  
We're working on an update to the Intune security baseline for Microsoft 365 Apps for Enterprise. This update will bring support for recent settings so you can continue to maintain best-practice configurations for Office apps.

For information about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../protect/security-baselines.md).


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
