---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: laurawi
ms.author: brenduns
manager: laurawi
ms.date: 08/21/2025
ms.topic: article
ms.service: microsoft-intune
ms.subservice: fundamentals
 
# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
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

### Endpoint Privilege Management Dashboard for user readiness and elevation trends<!-- 26123334 -->

We’re working on a dashboard for Endpoint Privilege Management (EPM) that brings you insights to support having your users run as standard users in place of running with local admin permissions. First, the dashboard will report progress towards a Standard User Status to help you understand when your admin users might be ready to be moved to standard users. The dashboard will also help you understand the file elevation trends in your organization.

<!-- ***********************************************-->

## App management

### Offline Mode and Pre-Signed In Apps for Android Enterprise Dedicated Devices<!-- 30303710, 25476290 -->

We're enhancing support for Android Enterprise dedicated devices with two new features in Managed Home Screen (MHS): Offline mode and App access without sign in.

Offline Mode lets users access designated apps when the device is offline or unable to connect to the network. You can also configure a grace period before requiring users to sign in once connectivity is restored.

App access without sign in lets users launch specific apps from the MHS sign-in screen--regardless of network status--via the MHS top bar. This can be helpful for apps that need to be available immediately, such as help desk or emergency tools.

These features are intended for use on dedicated devices enrolled in Microsoft Entra Shared device mode and will be configurable via device configuration policy.

Applies to:
- Android Enterprise

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

<!-- ## Device configuration -->


<!-- *********************************************** -->

## Device enrollment

### Intune to support Ubuntu 22.04 and later<!-- 32756619 -->

Microsoft Intune and the Microsoft Intune app for Linux will support Ubuntu 22.04 and later, while ending support for Ubuntu 20.04. Devices that are currently enrolled on Ubuntu 20.04 remain enrolled even when that version is no longer supported. New devices will be unable to enroll if they're running Ubuntu 20.04. To prepare for this change, check your Intune reporting to see what devices or users might be affected. In the admin center, go to **Devices** > **All devices** and filter OS by Linux. You can add more columns to help identify who in your organization has devices running Ubuntu 20.04. Notify your users to upgrade their devices to a supported Ubuntu version.

<!-- *********************************************** -->

## Device management

### Configure Windows Backup for Organizations (public preview)<!-- 29202026 -->

Intune administrators will be able to configure a new feature in public preview called Windows Backup for Organizations. With this feature, you can back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device. Backup settings will be configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device will be available in the admin center under **Enrollment**. For more information about this feature, see [Announcing Windows Backup for Organizations - Windows IT Blog](https://techcommunity.microsoft.com/blog/windows-itpro-blog/announcing-windows-backup-for-organizations/4416659).

<!-- *********************************************** -->

## Device security

### Security Baseline for audits of Security Technical Implementation Guides<!-- 31532934 -->

We’re adding a new security baseline that audits devices against the recommended configuration of Security Technical Implementation Guides (STIGs). As a baseline focused on audits and not on configuration, this baseline focuses on Windows devices, and generates detailed reports on which devices meet the recommended settings for compliance with STIGs.
 
Applies to:
- Windows

For information about the currently available Intune security baselines, see [Security baselines overview](../protect/security-baselines.md).

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

Applies to the following when you use the *Windows* platform:

- Windows 10
- Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Monitor and troubleshoot -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

## Role-based access control

### Multi-administrator approval support for role-based access control <!-- 26838684 -->

Support for multiple administrative approval (MAA) is being expanded to include role-based access control. When this feature is enabled, any changes to roles, including modifications to role permissions, admin groups, or member group assignments, require a second administrator to approve the change before it's applied. This helps protect your organization from unauthorized or accidental role-based access control changes by enforcing dual authorization.

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
