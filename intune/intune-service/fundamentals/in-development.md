---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
author: brenduns
ms.author: brenduns
ms.date: 04/02/2026
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

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../fundamentals/use-docs.md#notifications).
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

### Scope tags support for Endpoint Privilege Management reports<!-- 34630681 -->

We're fixing how scope tags work with Endpoint Privilege Management (EPM) reports. With this change, EPM reports will respect the report viewers assigned scope and display the details for only the users and devices that the report user is scoped to view.  

### Expanded support for Endpoint Privilege Management support approved elevation requests<!-- 33479618 -->

Soon Endpoint Privilege Management (EPM) will support the use of [support approved elevation requests](/intune/intune-service/protect/epm-support-approved) by all users of a device. Today, requesting elevation that requires support approval is limited to the device's primary user or the user who enrolled the device. This update expands the utility of support approved elevations and helps to improve scenarios that involve shared devices.

<!-- ***********************************************-->

## App management

### Multiple managed accounts for app protection policies <!-- 3182632 -->

The Multiple Managed Accounts (MMA) feature for Intune mobile application management (MAM) will enable users to add and manage more than one managed account within a single app. With MMA, app protection policies will be enforced independently for each account, as defined by the admin. This capability will be especially useful for scenarios such as consultants working across organizations, company acquisitions, or users managing multiple mailboxes within the same tenant.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - Android

<!-- *********************************************** -->

<!-- ## Device configuration -->

<!-- *********************************************** -->

## Device enrollment

### Access management for Apple services<!-- 31209876  -->

You will be able to use Apple access management settings in Apple Business Manager and Apple School Manager to configure service access for Apple accounts on organization-owned devices. These controls will let you choose what devices users can sign in to and which apps and services are available to them. For more information about how Apple defines service access and Apple account permissions, see the [Apple Business Manager User Guide](https://support.apple.com/guide/apple-business-manager/customize-user-access-to-apps-and-services-axm53xk34bq/web)(opens Apple support site).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Microsoft Intune will support userless ADE for visionOS and tvOS devices<!-- 29219451 -->

Microsoft Intune will be adding support for userless automated device enrollment (ADE) for visionOS and tvOS devices, enabling you to enroll and manage Apple Vision Pro and Apple TV through Apple Business Manager or Apple School Manager. This capability will support ADE without user affinity and includes custom configuration uploads for settings, default enrollment restrictions, and remote device actions. The feature will be available with Microsoft Intune Plan 2 as part of the Microsoft 365 Suite. Enrolled visionOS and tvOS devices will appear alongside iOS and iPadOS devices in the Intune admin center within **Apple mobile** and can be filtered. Support will require tvOS 26 and later or visionOS 26 and later. We recommend that you keep these devices up to date to receive the latest security fixes.

<!-- *********************************************** -->

## Device management

### Device page in the Intune admin center is updated (public preview) <!-- 3646300 16532161 -->

In the Intune admin center, when you go to **Devices** > **All Devices** and select a device, you'll notice a new full-page layout that gives you a single view of the device. Use this view to:

- Track device activity
- Access tools and reports
- Manage device information

The single device page has the following tabs:

- **Device action status**: Shows requested, in‑progress, and recently completed device actions. You can search, sort, and filter this list. You'll be able to quickly understand what actions are running or have completed without leaving the device view.
- **Tools + reports**: This tab was previously called **Overview**. It shows monitoring reports, lists, and tools, like remediations, that were previously accessed in another part of the admin center.
- **Properties**: Contains admin‑modifiable device properties with visible scope tags and a dedicated editing view.
- **Device details**: This was previously called **Hardware**. It provides physical device information and key Intune and Microsoft Entra management details.

Other features:

- Device actions are grouped, ordered, and labeled consistently across platforms and device types, with improved logic to show only relevant and permitted actions. Destructive actions are clearly separated and require confirmation, reducing unintentional actions.

- The updated layout uses a standard structure across device types and platforms, while adapting to platform‑specific capabilities.

- Improved labeling, hierarchy, and formatting make device information easier to scan and understand. **Essentials** elevates important device information and is accessible from any tab.

All existing device management capabilities remain available. This update focuses on making them easier to find and use.

### New TeamViewer connector experience in Microsoft Intune<!-- 35094013 -->

Microsoft Intune will update its TeamViewer integration to simplify onboarding and improve reliability for remote assistance workflows. The new connector will replace the existing TeamViewer connector experience and provide a more streamlined experience in the Intune admin center. After the older experience is retired, organizations using that TeamViewer connector will need to migrate to the new connector within 12 months to maintain functionality.

### New remote actions to suspend and restore Managed Home Screen on Android devices<!-- 10741483 -->

Intune will soon include two new remote actions that let admins temporarily suspend and later restore managed home screen (MHS) on Android devices. These actions allow users to exit MHS and access the device's default launcher for a specified duration, without removing policies or requiring a PIN.

After the defined time elapses, or when the *restore managed home screen* action is triggered, MHS is automatically restored, helping maintain device security while minimizing disruption.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)

<!-- *********************************************** -->

## Device security

### Security Baseline for audits of Security Technical Implementation Guides<!-- 31532934 -->

We're adding a new security baseline that audits devices against the recommended configuration of Security Technical Implementation Guides (STIGs).

The new baseline will be available for [US Government Community Cloud High (GCC High)](/intune/intune-service/fundamentals/intune-govt-service-description) tenants, and focused on audits and not on configuration. Applicable to Windows devices, the baseline generates detailed reports on which devices meet the recommended settings for compliance with STIGs.

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
