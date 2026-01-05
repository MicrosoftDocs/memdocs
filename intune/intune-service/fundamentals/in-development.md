---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
author: brenduns
ms.author: brenduns
ms.date: 01/07/2026
ms.topic: article
ms.reviewer: intuner
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description moves from this article to [What's new](whats-new.md).
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories: use this order:
## Microsoft Intune Suite
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

## Microsoft Intune Suite

### Expanded support for Endpoint Privilege Management support approved elevation requests<!-- 33479618 -->

Soon Endpoint Privilege Management (EPM) will support the use of [support approved elevation requests](/intune/intune-service/protect/epm-support-approved) by all users of a device. Today, requesting elevation that requires support approval is limited to the device’s primary user or the user who enrolled the device. This update expands the utility of support approved elevations and helps to improve scenarios that involve shared devices.

<!-- ***********************************************-->

## App management

### Lenovo Device Orchestration (LDO) link in the Intune admin center <!-- 32634377 -->

Microsoft Intune continues to expand its **Partner portals** experience, giving admins a single, secure interface to manage devices across multiple OEM ecosystems. A new integration is in development to provide a direct link to Lenovo Device Orchestration (LDO) from the Intune admin center.

When this feature becomes available, IT admins will be able to open the Lenovo Device Orchestration Portal directly from the Intune admin center to use Lenovo-specific management capabilities for supported devices.

> [!div class="checklist"]
> Applies to:
>
> - Windows 11

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### Filter by Android management mode in the settings catalog<!-- 31844205 -->

The [settings catalog](../configuration/settings-catalog.md) includes hundreds of settings that you can configure. There are built-in features that help filter the available settings.

When you create an Android settings catalog policy, there's a management mode filter option that filters the available settings by their enrollment type, including:

- Fully managed (COBO)
- Corporate-owned work profile (COPE)
- Dedicated (COSU)

To learn more about the settings catalog, see:

- [Android Intune settings catalog settings list](/configuration/settings-catalog-android.md)
- [Use the Intune settings catalog to configure settings](../configuration/settings-catalog.md)

### Apple declarative device management (DDM) supports assignment filters<!-- 24298491 -->

You'll be able to use assignment filters in policy assignments for DDM-based configurations, like software updates.

To learn more about filters, see [Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune](filters.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Recovery Lock settings catalog settings are available for macOS<!-- 32541429 -->

On macOS devices, you can configure a recovery OS password that prevents users from booting company-owned devices into recovery mode, reinstalling macOS, and bypassing remote management.

In a [settings catalog](../configuration/settings-catalog.md) policy, you can use the Recovery Lock settings to:

- Set a recovery lock password
- Configure a password rotation schedule
- Clear a recovery lock password

> [!div class="checklist"]
> Applies to:
>
> - macOS

<!-- *********************************************** -->

 <!--## Device enrollment -->  

<!-- *********************************************** -->

## Device management

### More options for assignment filters > Device Management Type property for managed apps on Android and iOS/iPadOS<!-- 25040926 -->

When you create policies for your managed apps, you can use [assignment filters](filters.md) to assign policies based on rules you create. In these rules, you can use different device and app properties, including the **Device Management Type** property on Android and iOS/iPadOS.

For Android, the **Device Management Type** property for managed apps is adding the following options:

- Corporate-owned with work profile
- Corporate-owned fully managed
- Corporate-owned dedicated devices without Entra ID Shared mode

For iOS/iPadOS, the **Device Management Type** property for managed apps is adding the following options:

- Automated Device Enrollment user-associated devices
- Automated Device Enrollment userless devices
- Account Driven User Enrollment
- Device Enrollment with Company Portal and Web Enrollment

To learn more about filters, see:

- [Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune](filters.md)
- [App and device properties, operators, and rule editing when creating assignment filters in Microsoft Intune](filters-device-properties.md)

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise
> - iOS/iPadOS

### Intune certificate inventory integration with Zimperium mobile threat defense<!-- 35519603 -->

You'll soon be able to configure certificate inventory sync as part of the Mobile Threat Defense (MTD) connector setup when using Zimperium. This enhancement will help you detect when the device threat level is elevated due to approved but potentially malicious certificates on the device. The setting can be configured for Intune to send certificate inventory for corporate and personally owned devices to Zimperium.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

<!-- *********************************************** -->

## Device security

### Updated firewall configurations for new Intune network endpoints<!-- 34445623 -->

As part of Microsoft's ongoing [Secure Future Initiative (SFI)]( https://www.microsoft.com/trust-center/security/secure-future-initiative), network service endpoints for Microsoft Intune will be moving to new IP addresses. As a result, customers might need to update network (firewall) configurations in third-party applications to enable proper function of Intune device and app management. This change will affect customers using a firewall allow list that allows outbound traffic based on IP addresses or Azure service tags.

### Security Baseline for audits of Security Technical Implementation Guides<!-- 31532934 -->

We're adding a new security baseline that audits devices against the recommended configuration of Security Technical Implementation Guides (STIGs). As a baseline focused on audits and not on configuration, this baseline focuses on Windows devices and generates detailed reports on which devices meet the recommended settings for compliance with STIGs.

> [!div class="checklist"]
> Applies to:
>
> - Windows

For information about the currently available Intune security baselines, see [Security baselines overview](../protect/security-baselines.md).

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

> [!div class="checklist"]
> Applies to the following when you use the *Windows* platform:
>
> - Windows 10
> - Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->


<!-- ## Monitor and troubleshoot -->


<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
