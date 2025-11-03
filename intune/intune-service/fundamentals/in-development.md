---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
author: brenduns
ms.author: brenduns
ms.date: 10/27/2025
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

### More volume options available in Managed Home Screen<!-- 16462284 -->

We're adding more volume control options to the Managed Home Screen (MHS) app for Android Enterprise dedicated and fully managed devices. With this update, you can enable additional controls for call, ring, notification, and alarm volumes, giving users greater flexibility to adjust sound levels based on their needs.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise (dedicated and fully managed devices)

### Reset Managed Google Play store mode to Basic<!-- 33632857 -->

You'll soon be able to reset the Managed Google Play store layout from *Custom* back to *Basic* in the Intune admin center under **Apps** > **All apps** > **Create Managed Google Play app**.

In **Basic** mode, all approved apps are visible to users. In **Custom** mode, newly approved apps must be added to collections. When you reset to Basic, Intune deletes all existing collections. The **Reset to Basic** button appears only when the store is in Custom mode and shows immediate success or failure.
 
> [!div class="checklist"]
> Applies to:
>
> - Android

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### Settings available in both Templates and Settings Catalog for Android Enterprise <!-- 34876806 -->

Some settings that were only available in Templates are now also supported in the settings catalog.

The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

To create a new settings catalog policy, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type.

The following settings are available in the settings catalog:

**General**:

- Skip first use hints
- Contact sharing via Bluetooth (work profile level)
- Search work contacts and display work contact caller-id in personal profile
- Data sharing between work and personal profiles

**Work profile password**:

- Required password type
- Minimum password length
- Number of characters required
- Number of lowercase characters required
- Number of uppercase characters required
- Number of non-letter characters required
- Number of numeric characters required
- Number of symbol characters required
- Number of days until password expires
- Number of passwords required before user can reuse a password
- Number of sign-in failures before wiping device
- Required unlock frequency

To learn more about these settings, go to [Android Intune settings catalog settings list](../configuration/settings-catalog-android.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

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

### New Assist Content Sharing setting in the Android Enterprise settings catalog<!-- 31479342  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type):

- **Block assist content sharing with privileged apps**: If **True**, this setting blocks assist content, like screenshots and app details, from being sent to a privileged app, like an assistant app. The setting can be used to block the **Circle to Search** AI feature.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
> - Android Enterprise corporate owned fully managed (COBO)
> - Android Enterprise corporate owned dedicated devices (COSU)

<!-- *********************************************** -->

## Device enrollment

### New opt-in upgrade to allow existing customers to move from managed Google Play Accounts to Microsoft Entra ID accounts  <!-- 30675087 -->

Microsoft Intune will offer a new opt-in upgrade that allows existing Android Enterprise customers to move from using managed Google Play accounts to using Microsoft Entra ID accounts for Android device management. Customers are eligible if they previously used a managed Google Play account. This better together enterprise (BTE) integration streamlines the onboarding process by eliminating the need for a separate Google account and leveraging your work account. It's not required to switch account types. 

To learn more about this change, see [New onboarding flow to managing Android Enterprise devices with Microsoft Intune](https://techcommunity.microsoft.com/blog/intunecustomersuccess/new-onboarding-flow-to-managing-android-enterprise-devices-with-microsoft-intune/4206602).


### New Setup Assistant screens to be generally available for iOS/iPadOS and macOS automated device enrollment profiles <!-- 29832295, 29611787 -->

As an IT admin, you'll be able to hide or show 12 new Setup Assistant screens during automated device enrollment (ADE). The default is to show these screens during Setup Assistant.

The screens you can skip during iOS/iPadOS enrollment, and the applicable versions include:
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

### Configure Windows Backup for Organizations<!--29202026 -->

A new feature called *Windows Backup for Organizations* will soon be generally available in Microsoft Intune. With this feature, you can back up your organization's Windows settings and restore them on a Microsoft Entra joined device. Backup settings will be configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device will be available in the admin center under **Enrollment**. For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../enrollment/windows-backup-restore.md).

<!-- *********************************************** -->

## Device management

### Windows Autopilot device preparation in automatic mode to be available for Windows 365 Enterprise, Windows 365 Frontline in dedicated mode, and Windows 365 Cloud Apps (public preview)<!-- 35518695 -->

You will be able to use Windows Autopilot device preparation policies in automatic flow to provision Windows 365 Enterprise, Windows 365 Frontline in dedicated mode, and Windows 365 Cloud Apps. The policy can be included in the Cloud PC provisioning policy and will apply immediately after the Cloud PCs are created to deliver apps and scripts to the device before a user logs in. You'll be able to monitor deployment status in the [Windows Autopilot device preparation deployment report](/autopilot/device-preparation/reporting-monitoring).

For a tutorial, see [Step by step tutorial for Windows Autopilot device preparation in automatic mode for Windows 365 in Intune](/autopilot/device-preparation/tutorial/automatic/automatic-workflow).

For more information, see the following articles:

- [Create provisioning policies for Windows 365 | Microsoft Learn](/windows-365/enterprise/create-provisioning-policy)
- [Windows 365 Cloud Apps | Microsoft Learn](/windows-365/enterprise/cloud-apps)
- [Use Autopilot device preparation with Cloud PCs | Microsoft Learn](/windows-365/enterprise/autopilot-device-preparation)

### New prompts available to explore your Intune data<!-- 33787582 -->

You can use Security Copilot in Intune to explore new prompts related to your data using natural language. Use these new prompts to view data on:

- Users and groups
- Role based access control (RBAC)
- Audit logs

When you start typing your request, a list of prompts that best match your request are shown. You can also continue typing for more suggestions.

Each query returns a Copilot summary to help you understand the results and offers suggestions. With this information, you can also:

- Add devices or users from the results to a group so you can target apps and policies to this group.
- Filter example queries to find or build requests that match your needs.

To learn more, see [Explore Intune data with natural language and take action](../copilot/copilot-intune-explorer.md).

### Device Management type assignment filter property supports more Android enrollment options<!-- 33016364 -->

When you create a policy in Intune, you can use [assignment filters](filters.md) to assign a policy based on rules you create. You can create a rule using different [app properties](filters-device-properties.md), like `deviceManagementType`.

The Device Management Type property supports the following Android enrollment options for managed devices:

- Corporate-owned dedicated devices with Entra ID Shared mode
- Corporate-owned dedicated devices without Entra ID Shared mode
- Corporate-owned with work profile
- Corporate-owned fully managed
- Personal-owned device with a work profile
- AOSP user-associated devices
- AOSP userless devices

To learn more about filters and the properties you can currently use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [App and device properties, operators, and rule editing when creating filters in Microsoft Intune](filters-device-properties.md)

> [!div class="checklist"]
> Applies to:
>
> - Android

<!-- *********************************************** -->

## Device security

### Microsoft Tunnel for detection and protection for rooted Android devices<!-- 30336962 -->

We’re updating Microsoft Tunnel with the capability to detect and block access from rooted Android devices. This update will ensure that only compliant and trustworthy devices can establish secure connections through the Tunnel.
 
This new capability will be available with Microsoft Tunnel for [Mobile Device Management](/intune/intune-service/protect/microsoft-tunnel-overview) (MDM) and for [Mobile Application Management](/intune/intune-service/protect/microsoft-tunnel-mam) (MAM).

### Updated firewall configurations for new Intune network endpoints<!-- 34445623 -->

As part of Microsoft's ongoing [Secure Future Initiative (SFI)]( https://www.microsoft.com/trust-center/security/secure-future-initiative), network service endpoints for Microsoft Intune will be moving to new IP addresses. As a result, customers might need to update network (firewall) configurations in third-party applications to enable proper function of Intune device and app management. This change will affect customers using a firewall allowlist that allows outbound traffic based on IP addresses or Azure service tags.

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
