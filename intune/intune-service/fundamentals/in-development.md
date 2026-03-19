---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
author: brenduns
ms.author: brenduns
ms.date: 03/26/2026
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

### Declarative Device Management for Apple line-of-business apps on iOS/iPadOS<!-- 30457044 -->

We're adding support for Declarative Device Management (DDM) in Microsoft Intune for configuring required line-of-business (LoB) apps on devices running iOS/iPadOS 18 and later.

Apple's new Managed App configuration introduces policy-based app deployment and configuration using the declarative management model. This allows for efficient app delivery, real-time app status, and expanded app attribute options for per-app associated domains.

Admins can configure line-of-business apps to use DDM by changing the management type setting in App information.

### Multiple managed accounts for app protection policies <!-- 3182632 -->

The Multiple Managed Accounts (MMA) feature for Intune mobile application management (MAM) will enable users to add and manage more than one managed account within a single app. With MMA, app protection policies will be enforced independently for each account, as defined by the admin. This capability will be especially useful for scenarios such as consultants working across organizations, company acquisitions, or users managing multiple mailboxes within the same tenant.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - Android

<!-- *********************************************** -->

## Device configuration

#### New supported OEMConfig app for Android Enterprise <!-- 36423115 -->

The following OEMConfig app is available in Intune for Android Enterprise:

- Inventus | `com.inventus.oemconfig.gen`

For more information about OEMConfig, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

<!-- *********************************************** -->

## Device enrollment

### Access management for Apple services<!-- 31209876 iddraft idready idstaged -->

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

### New TeamViewer connector experience in Microsoft Intune<!-- 35094013 -->

Microsoft Intune will update its TeamViewer integration to simplify onboarding and improve reliability for remote assistance workflows. The new connector will replace the existing TeamViewer connector experience and provide a more streamlined experience in the Intune admin center. After the older experience is retired, organizations using that TeamViewer connector will need to migrate to the new connector within 12 months to maintain functionality.

<!-- *********************************************** -->

## Device security

### New settings in the Windows settings catalog <!-- 34444997 -->

There will be new maintenance window settings for OS, drivers, and updates in the Windows settings catalog. You'll be able configure the type of updates that should take place (Download, install, restart), start date, time, duration and repeat schedule.

To see and configure these settings in Intune, create a Windows settings catalog profile (**Devices > Configuration profiles > Create profile > Windows 10 and later > Settings catalog**).

The new policies will include:

- Enable Maintenance windows (On/Off)
- Update action (Download, install, restart options)
- Start date
- Start time
- Duration (hours)
- Repeat schedule
- Weekly – Day selection
- Monthly – schedule type
- Monthly – Day of the month
- Monthly – Occurrence in month - Week
- Monthly – Occurrence in month - Day of the week

> [!div class="checklist"]
> Applies to:
>
> - Windows

To learn more about the settings catalog, see [Use the Intune settings catalog to configure settings](../configuration/settings-catalog.md).

### Intune security baseline for Windows 11 version 25H2 <!-- 34955665 -->

We're working on an updated Windows security baseline for Windows 11, version 25H2, to reflect the latest Microsoft security recommendations for supported Windows devices. The update is expected to introduce changes such as new settings, updated default values, and the retirement of existing settings to align with current Windows security guidance.

When available, the 25H2 baseline will be provided as a new baseline version. Existing baseline profiles won't automatically update to the new version.

For more information about the security baseline changes introduced with Windows 11, version 25H2, see the Windows blog: [Windows 11, version 25H2 security baseline](https://techcommunity.microsoft.com/blog/microsoft-security-baselines/windows-11-version-25h2-security-baseline/4456231). To prepare for updating a baseline in Intune, see [Configure security baseline policies in Microsoft Intune](../protect/security-baselines-configure.md#update-a-baseline-profile-to-the-latest-version).

> [!div class="checklist"]
> Applies to:
>
> - Windows 11

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

## Tenant administration

### Guided scenarios being removed from the Intune admin center <!-- 29654118 -->

All guided scenarios except Windows 365 Boot will be removed from the Microsoft Intune admin center. After this change, you'll no longer be able to access the guided scenario wizards. However, any Intune objects previously created by these wizards, such as policies and apps, will remain and can continue to be managed as usual. The Windows 365 Boot guided scenario will remain available and can be accessed from the Windows 365 overview page in the Intune admin center. No action is required to prepare for this change.

For alternative step-by-step guidance, see the following resources:

- [Microsoft Intune documentation](https://go.microsoft.com/fwlink/?linkid=2310495)
- I[ntune prescriptive guides](https://go.microsoft.com/fwlink/?linkid=2300666)
- Intune administration guides: [https://m365accelerator.microsoft.com/intune](https://m365accelerator.microsoft.com/intune)
  - [Securing apps for mobile | Android](https://m365accelerator.microsoft.com/intune/manage-and-secure-apps-for-android)
  - [Securing apps for mobile | iOS](https://m365accelerator.microsoft.com/intune/manage-and-secure-apps-for-ios)
  - [Configuring Intune and Configuration Manager to co-manage devices](https://m365accelerator.microsoft.com/intune/microsoft-intune-and-configuration-manager-co-management-setup-guide)
  - [Manage and secure devices for Windows](https://m365accelerator.microsoft.com/intune/windows-device-management)
- [Microsoft Copilot in Intune](/intune/intune-service/copilot/copilot-intune-overview)

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
