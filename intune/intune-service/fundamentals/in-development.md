---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
author: brenduns
ms.author: brenduns
ms.date: 02/12/2026
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

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### Apple declarative device management (DDM) support for assignment filters<!-- 24298491 -->

You'll be able to use assignment filters in policy assignments for DDM-based configurations, like software updates.

To learn more about filters, see [Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune](filters.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Recovery Lock settings catalog settings for macOS<!-- 32541429 -->

On macOS devices, you can configure a recovery OS password that prevents users from booting company-owned devices into recovery mode, reinstalling macOS, and bypassing remote management.

In a [settings catalog](../configuration/settings-catalog.md) policy, you can soon use the Recovery Lock settings to:

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

### Multi-administrator approval support for device compliance and device configuration policies<!-- 26838614 -->

Multi-administrator approval will soon support device configuration policies created through the settings catalog, device compliance policies, compliance settings, and device cleanup rules. When you turn on this feature, any changes you make, including creating, editing, or deleting a policy, must be approved by a second administrator before they take effect. This dual-authorization process helps protect your organization from unauthorized or accidental changes to role-based access control.

<!-- *********************************************** -->

## Device security

### Autopatch update readiness<!--34573480 -->

Autopatch update readiness will deliver a unified experience for tracking and remediating Windows update issues across Intune‑enrolled devices and Autopatch group‑enrolled devices.

This experience will provide complete Intune-enrolled device accounting, enabling admins to view all managed devices, their enrollment status, and their policy assignments in a single dashboard.

Autopatch update readiness will include the following capabilities:

- A *device update journey* that surfaces granular update states for each device, making it easier to identify where updates stall and why.
- A *centralized alerting framework* that consolidates actionable alerts for update failures, policy conflicts, and readiness gaps, with remediation guidance integrated into a single dashboard.
- An *update readiness checker* that enables admins to proactively evaluate devices for deployment risks and flag devices as *At Risk* based on signals like disk space, appraiser data, and setup conditions.
- *Repair Devices with OS Reinstall*, a capability that enables admins to remediate upgrade‑blocked devices by triggering an OS reinstall for common issues such as insufficient disk space and app compatibility problems, with supporting alerts and reporting.

> [!div class="checklist"]
> Applies to:
>
> - Windows

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

## Monitor and troubleshoot

### Operator updates for device query for multiple devices<!--36180651 -->

The following operator and behavior changes will be coming to **Device query for multiple devices**.

- **New join types**\
  The following join types will be supported:
  - `leftsemi`
  - `rightsemi`
  - `leftanti`
  - `rightanti`

- **Changes to join behavior**\
  Joins that use `on Device.DeviceID` will no longer be supported. Queries that currently use `on Device.DeviceId` should switch to using `on Device`, or omit the `on` clause entirely.

- **Changes to device references in operators**\
  Using `Device` by itself will no longer be valid in operators such as `distinct`, `summarize`, or `order by`. Queries will need to reference a specific device property instead.

- **Updates to query results**\
  Queries that involve a device—either by querying a device directly or by joining a device to another entity—will return the device as a clickable link in the results, allowing navigation to the device details.

- **Improved error messages**\
  Some error cases have been updated to provide clearer, more descriptive messages.

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
