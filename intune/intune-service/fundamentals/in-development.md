---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: laurawi
ms.author: brenduns
manager: laurawi
ms.date: 09/17/2025
ms.topic: article
ms.service: microsoft-intune
ms.subservice: fundamentals
 
# optional metadata

#audience:

ms.reviewer: intuner
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

Endpoint Privilege Management (EPM) will soon offer a new option for elevation rules: the ability to run elevated applications using the user's context, not just a virtual account. Today, when EPM elevates an app or file, it uses a virtual account for security. While this protects your environment, it can result in elevated apps missing a users personal settings, preferences, and customizations.
 
With this upcoming change, EPM elevation rules will support changing the user token context. This means that when EPM runs an app with elevated privileges, a users personalized experience like custom file paths, app settings, and preferences can be preserved by the EPM elevation.

For more information, see [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-overview.md).

### Endpoint Privilege Management Dashboard for user readiness and elevation trends<!-- 26123334 -->

We're working on a dashboard for Endpoint Privilege Management (EPM) that brings you insights to support having your users run as standard users in place of running with local admin permissions. First, the dashboard will report progress towards a Standard User Status to help you understand when your admin users might be ready to be moved to standard users. The dashboard will also help you understand the file elevation trends in your organization.

<!-- ***********************************************-->

## App management

### PowerShell script support when installing Win32 apps<!-- 29857395 -->

For added flexibility when installing apps, you'll be able to upload a PowerShell script to install Enterprise App Catalog apps as an alternative to running a command line. Support for other Win32 app types will be added soon.

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

<!-- *********************************************** -->

<!-- ## Device configuration -->


<!-- *********************************************** -->

## Device enrollment

### Configure Windows Backup for Organizations<!--29202026 -->

A new feature called *Windows Backup for Organizations* will be soon be generally available in Microsoft Intune. With this feature, you can back up your organization's Windows settings and restore them on a Microsoft Entra joined device. Backup settings will be configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device will be available in the admin center under **Enrollment**. For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../enrollment/windows-backup-restore.md). 

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

<!-- *********************************************** -->

## Device security

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
