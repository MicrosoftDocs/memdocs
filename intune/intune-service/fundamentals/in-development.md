---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
author: brenduns
ms.author: brenduns
ms.date: 10/13/2025
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

### Support for user account context in Endpoint Privilege Management Elevation Rules<!-- 25617968 -->

Endpoint Privilege Management (EPM) will soon offer a new option for elevation rules: the ability to run elevated applications using the user's context, not just a virtual account. Today, when EPM elevates an app or file, it uses a virtual account for security. While this feature protects your environment, it can result in elevated apps missing a users personal settings, preferences, and customizations.

With this upcoming change, EPM elevation rules will support changing the user token context. This means that when EPM runs an app with elevated privileges, a users personalized experience like custom file paths, app settings, and preferences can be preserved by the EPM elevation.

For more information, see [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-overview.md).

### Endpoint Privilege Management Dashboard for user readiness and elevation trends<!-- 26123334 -->

We're working on a dashboard for Endpoint Privilege Management (EPM) that brings you insights to support having your users run as standard users in place of running with local admin permissions. First, the dashboard will report progress towards a Standard User Status to help you understand when your admin users might be ready to be moved to standard users. The dashboard will also help you understand the file elevation trends in your organization.

<!-- ***********************************************-->

## App management

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### Support for SystemInfo entity<!-- 30326613 -->

*SystemInfo* will be added as a new entity designed to support multiple-device queries in the Intune data platform within resource explorer. It will enable system-level device insights, such as OS version, hardware details, and configuration state, within a single query. The new entity will improve reporting accuracy, streamline diagnostics, and enhance support workflows without requiring changes from you or your end users.

### New Assist Content Sharing setting in the Android Enterprise settings catalog<!-- 31479342 idready -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type):

- **Block assist content sharing with privileged apps**: If **True**, this setting blocks assist content, like screenshots and app details, from being sent to a privileged app, like an assistant app. The setting can be used to block the **Circle to Search** AI feature.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
> - Android Enterprise corporate owned fully managed (COBO)
> - Android Enterprise corporate owned dedicated devices (COSU)

### New Wi-Fi Direct setting in the Android Enterprise settings catalog <!-- 31495587 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type):

- **Block Wi-Fi Direct**: If **True**, this setting blocks Wi-Fi Direct, which is a direct, peer-to-peer connection between devices using Wi-Fi frequencies.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE)
> - Android Enterprise corporate owned fully managed (COBO)
> - Android Enterprise corporate owned dedicated devices (COSU)

### Hide organization name setting supported on Android Enterprise corporate owned single use dedicated devices<!-- 34438509 -->

The **Hide organization name** settings catalog setting now supports corporate owned single use dedicated devices (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type).

Previously, this setting was only supported on corporate-owned devices with a work profile and corporate owned fully managed devices.

For more information on this setting, see [Android Enterprise device settings list in the Intune settings catalog](../configuration/settings-catalog-android.md).

### Settings available in both Templates and Settings Catalog for Android Enterprise<!-- 34458121 -->

Some settings that were only available in Templates are now also supported in the settings catalog.

The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

To create a new settings catalog policy, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type.

The following settings are available in the settings catalog:

**General**:

- Block screen capture (work profile-level)
- Block mounting of external media
- Block location
- Microphone adjustment
- Block date and time changes
- Allow network escape hatch
- Allow USB storage
- Block access to status bar
- Block Wi-Fi setting changes
- Notification windows
- Allow copy and paste between work and personal profiles

To learn more about these settings, go to [Android Intune settings catalog settings list](../configuration/settings-catalog-android.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

<!-- *********************************************** -->

## Device enrollment

### New Setup Assistant screens to be generally available for iOS/iPadOS and macOS automated device enrollment profiles <!-- 29832295, 29611787 -->

As an IT admin, you'll be able to hide or show 12 new Setup Assistant screens during automated device enrollment (ADE). The default is to show these screens during Setup Assistant.

The screens you can skip during iOS/iPadOS enrollment, and the applicable versions, include:
- **App Store** (iOS/iPadOS 14.3+)
- **Camera button** (iOS/iPadOS 18+)
   - **Web content filtering** (iOS/iPadOS 18.2+)
   - **Safety and handling** (iOS/iPadOS 18.4+)
   - **Multitasking** (iOS/iPadOS 26+)
   - **OS Showcase** (iOS/iPadOS 26+)

The screens you can skip during macOS enrollment include:
- **App Store** (macOS 11.1+)
- **Get Started** (macOS 15+)
- **Software update** (macOS 15.4+)
- **Additional privacy settings** (macOS 26+)
- **OS Showcase** (macOS 26+)
- **Update completed** (macOS 26+)
- **Get Started** (macOS 15+)

### Edit Managed Google Play organization name<!--32268351 -->

You will be able to edit the Managed Google Play organization name directly in the Intune admin center under **Devices** > **Android** > **Enrollment** > **Managed Google Play**. The updated name, which will be validated on input, will appear in the admin center. It might also appear on Android device lock screens within a message like *This device is managed by [organization name]*.

### Configure Windows Backup for Organizations<!--29202026 -->

A new feature called *Windows Backup for Organizations* will be soon be generally available in Microsoft Intune. With this feature, you can back up your organization's Windows settings and restore them on a Microsoft Entra joined device. Backup settings will be configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device will be available in the admin center under **Enrollment**. For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../enrollment/windows-backup-restore.md).

<!-- *********************************************** -->

## Device security

### Intune to end support for legacy Apple MDM software updates<!-- 33004946 -->

With the release of iOS 26, iPadOS 26, and macOS 26, Apple has deprecated legacy mobile device management (MDM) software update commands and payloads. To align with this change, Intune will soon end support for the following MDM-based workloads:

- iOS/iPadOS update policies
- macOS update policies
- Software update settings in:
  - iOS/iPadOS **templates** > **Device restrictions**
  - iOS/iPadOS **settings catalog** > **Restrictions**
  - macOS **templates** > **Device restrictions**
  - macOS **settings catalog** > **Restrictions**
  - macOS **settings catalog** > **Software update**
- Reports:
  - iOS/iPadOS update installation failures
  - macOS update installation failures
  - macOS per-device software updates

These functionalities [are now available through declarative device management (DDM)](/intune/intune-service/protect/managed-software-updates-ios-macos), which provides a more modern and reliable approach to managing Apple software updates. For more information about this transition, see the Intune Customer Success blog [Move to declarative device management for Apple software updates](https://aka.ms/Intune/Apple-DDM-software-updates).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Updated firewall configurations for new Intune network endpoints<!-- 34445623 -->

As part of Microsoft's ongoing [Secure Future Initiative (SFI)]( https://www.microsoft.com/trust-center/security/secure-future-initiative), network service endpoints for Microsoft Intune will be moving to new IP addresses. As a result, customers might need to update network (firewall) configurations in third-party applications to enable proper function of Intune device and app management. This change will affect customers using a firewall allowlist that allows outbound traffic based on IP addresses or Azure service tags.

### Security Baseline for audits of Security Technical Implementation Guides<!-- 31532934 -->

We're adding a new security baseline that audits devices against the recommended configuration of Security Technical Implementation Guides (STIGs). As a baseline focused on audits and not on configuration, this baseline focuses on Windows devices, and generates detailed reports on which devices meet the recommended settings for compliance with STIGs.

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


## Monitor and troubleshoot

### Enrollment time grouping failure report to be generally available for Android and Windows <!-- 33290045 -->

Soon to be generally available in the Microsoft Intune admin center, the enrollment time grouping failures report shows failures, which include devices that failed to become a member of the specified static device group during one of the following processes:

- Windows Autopilot device preparation provisioning.
- Enrollment of Android Enterprise fully managed, corporate-owned work profile devices.
- Enrollment of Android Enterprise dedicated devices.

The enrollment time grouping failures report will be available in the admin center under **Devices** > **Monitor** > **Enrollment time grouping failures**. Recently updated information could take up to 20 minutes to appear in the report.

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
