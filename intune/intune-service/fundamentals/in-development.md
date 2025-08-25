---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: laurawi
ms.author: brenduns
manager: laurawi
ms.date: 08/25/2025
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

### Support for user account context in Endpoint Privilege Management Elevation Rules<!-- 25617968 -->

Endpoint Privilege Management (EPM) will soon offer a new option for elevation rules: the ability to run elevated applications using the user’s context, not just a virtual account. Today, when EPM elevates an app or file, it uses a virtual account for security. While this protects your environment, it can result in elevated apps missing a users personal settings, preferences, and customizations.
 
With this upcoming change, EPM elevation rules will support changing the user token context. This means that when EPM runs an app with elevated privileges, a users personalized experience like custom file paths, app settings, and preferences can be preserved by the EPM elevation.

For more information, see [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-overview.md).

### Endpoint Privilege Management Dashboard for user readiness and elevation trends<!-- 26123334 -->

We’re working on a dashboard for Endpoint Privilege Management (EPM) that brings you insights to support having your users run as standard users in place of running with local admin permissions. First, the dashboard will report progress towards a Standard User Status to help you understand when your admin users might be ready to be moved to standard users. The dashboard will also help you understand the file elevation trends in your organization.

<!-- ***********************************************-->

## App management

### PowerShell script support when installing Win32 apps<!-- 29857395 -->

For added flexibility when installing apps, you'll be able to upload a PowerShell script to install Enterprise App Catalog apps as an alternative to running a command line.

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### Filter device configuration profiles by the policy type<!-- 33223685 -->

In the Intune admin center > **Devices** > **Configuration**, you can use the **Add filters** feature to filter your list of policies by platform, scope tags, and the last modified date.

**Policy type** is now available in the **Add filters** feature. So, you can filter your list of policies by their type, like the settings catalog, custom, device restrictions, and the other policy types.

### New Private Space setting in the Android Enterprise settings catalog <!-- 30802944 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There's a new **Block private space** setting (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type). When set to **True**, users are prevented from creating or using private spaces on the device. All existing private spaces will be deleted.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../configuration/settings-catalog-android.md).

Applies to:

- Android Enterprise corporate-owned devices with a work profile (COPE)

### New USB access setting in the Android Enterprise settings catalog <!-- 24213820 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There's a new **USB access** setting (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type). The setting allows admins to select what files and/or data can be transferred via USB. If admins block file transfer, only files will be blocked from being transferred and other connection (such as mouse) will still be allowed. If admins block USB data transfer, all data will be blocked.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../configuration/settings-catalog-android.md).

Applies to:

- Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

### New day zero settings available in the Apple settings catalog <!-- 33806647 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.
 
#### iOS/iPadOS

**Managed Settings > Default Applications**:

- Calling
- Messaging

**Restrictions**:

- Allowed Camera Restriction Bundle IDs

**Web > Web Content Filter**:

- Safari History Retention Enabled

#### macOS

**Authentication > Extensible Single Sign On Kerberos**:

- Use Platform SSO TGT

**Microsoft Defender**:

- The Microsoft Defender category is updated with new settings. Learn more about available macOS Defender settings at [Microsoft Defender - Policies](/defender-endpoint/mac-preferences).

**Restrictions**:

- Allow Call Recording
- Allow Live Voicemail

**Web > Web Content Filter**:

- Safari History Retention Enabled

### Settings available in both Templates and Settings Catalog for Android Enterprise <!-- 34226745 -->

Settings that have previously been supported in Templates are now also supported in the settings catalog.

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

To create a new Settings Catalog policy, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type.

The following settings are in the settings catalog:

**General**:

- Block roaming data services
- Block Bluetooth configuration
- Block Wi-Fi access point configuration
- Default permission policy
- Block access to camera
- Allow access to developer settings
- Block beaming data from apps using NFC (work-profile level)

  > [!NOTE]
  > This setting is deprecated in A10, but the setting still configures correctly on newer devices. But, the setting doesn't do anything because the feature isn't available.

- Block factory reset
- Block tethering and access to hotspots
- Block volume changes

  > [!NOTE]
  > This setting shows as successfully applied to corporate-owned devices with a work profile. But, the setting has no effect.

**Users and accounts**:

- User can configure credentials (work profile-level)
- Block account changes

**System Security**:

- Require threat scan on apps
- Require Common Criteria mode

**Applications**:

- Allow installation from unknown sources
- App auto-updates (work profile-level)

Applies to:

- Android Enterprise

<!-- *********************************************** -->

## Device enrollment

### Configure Windows Backup for Organizations<!--29202026 -->

A new feature called *Windows Backup for Organizations* will be soon be generally available in Microsoft Intune. With this feature, you can back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device. Backup settings will be configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device will be available in the admin center under **Enrollment**. For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../enrollment/windows-backup-restore.md). 

<!-- *********************************************** -->

## Device management

### End of support for older versions of the Intune Company Portal app<!-- 33827426 -->

On October 1, 2025, support for all Intune Company Portal versions that are older than 5.0.5421.0 ends. When support ends, users with a device that runs an older version of the Intune Company Portal might not be able to successfully maintain that device's registration status and those devices could be identified as non-compliant. For devices to remain registered and in compliance, the Company Portal version must be updated to a version that remains in support.

To update the version of the Company Portal app, see the following available guidance:

**For administrators:**  
- Use Intune to deploy the latest version: [Windows Company Portal app by using Microsoft Intune](../apps/store-apps-company-portal-app.md)

**For device users:**  
- Get the latest version of the Company Portal from your device's app store:
  - [Apple App Store](https://apps.apple.com/app/intune-company-portal/id719171358)
  - [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)
  - [Microsoft Store](https://apps.microsoft.com/detail/9wzdncrfj3pz)

### Resource explorer renamed to Device inventory <!-- 33630406 -->

The **Resource explorer** pane under **Monitor** for Windows devices will be renamed to **Device inventory**. This change applies to tenants with at least one device targeted by a [properties catalog](/intune/intune-service/configuration/properties-catalog) policy. The experience and data remain unchanged—only the pane name is changed.

> [!div class="checklist"]
> Applies to:
>
> - Windows

> [!NOTE]
> The **Resource explorer** pane that displays Configuration Manager data via [tenant attach](/intune/configmgr/tenant-attach/resource-explorer) will retain its current name.

### New features in Copilot for Microsoft Intune <!-- 32549162 -->

- **Easier access to Copilot Chat** - Copilot Chat is embedded directly into the Intune admin center header. So, IT admins can access Copilot Chat from any screen in the admin center. This feature helps admins get faster insights and support.

- **Context-aware conversations with Copilot Chat** - As you type, a dynamic prompt box provides real-time suggestions and recommends prompts relevant to what you're trying to ask. You can troubleshoot devices, manage policies, explore Windows 365 features, and more. You can also directly access the Microsoft docs to learn more.

  Copilot Chat retains your conversation history and remains context aware as you move through the admin center. This continuity helps minimize repetitive prompts.

- **Expanded support for Windows 365 Cloud PC** - With this general availability update, Copilot now supports Windows 365 Cloud PC management. IT admins can access important info, like licensing status, connection quality, configuration details, and performance metrics. This feature makes it easier for admins to monitor and manage Cloud PCs directly from the Intune admin center.

<!-- *********************************************** -->

## Device security

### New security baseline update experience<!-- 31607281 -->

We’re updating the Intune security baseline update experience. With this change, when you choose to update an existing baseline to its newest baseline version, you’ll be able to choose between options to keep the customizations you’ve made, which will be applied to the new version instance, or to discard those customizations and create a new baseline instance using the baselines recommended values from the new version. With both options, the new version is created as a new baseline instance and the original baseline instance remains available until you choose to remove it from your tenant.
 
This change will apply to updates of baseline versions created after May 2023, which use a newer settings format that wasn't available in older security baseline versions.

### Updated firewall configurations for new Intune network endpoints<!-- 34445623 -->

As part of Microsoft’s ongoing [Secure Future Initiative (SFI)]( https://www.microsoft.com/trust-center/security/secure-future-initiative), network service endpoints for Microsoft Intune will be moving to new IP addresses. As a result, customers might need to update network (firewall) configurations in third-party applications to enable proper function of Intune device and app management. This change will affect customers using a firewall allowlist that allows outbound traffic based on IP addresses or Azure service tags.

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

## Monitor and troubleshoot

### Give feedback about multiple device query<!-- 33381301 -->

You will be able to use the new feedback feature on the multiple device query page to submit feedback about multiple device query.

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
