---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
ms.date: 05/01/2026
ms.topic: whats-new
ms.reviewer: intuner
ms.collection:
- M365-identity-device-management
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description moves from this article to [What's new](index.md).
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](index.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../fundamentals/use-docs.md#notifications).
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

### Scope tags support for Endpoint Privilege Management reports<!-- 34639681 -->

We're fixing how scope tags work with Endpoint Privilege Management (EPM) reports. With this change, EPM reports will respect the report viewers assigned scope and display the details for only the users and devices that the report user is scoped to view.  

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

## Device enrollment

### Complete Platform SSO registration during macOS Automated Device Enrollment<!-- 36767290 -->

On macOS devices enrolled with Automated Device Enrollment (ADE), you can enable and complete Platform SSO device registration:

- In a settings catalog policy, add and configure the `Enable Registration During Setup` setting, save your policy, and assign it to a static group.
- Configure the Automated Device Enrollment policy to use Setup Assistant with modern authentication and enable await final configuration. 
- During enrollment, users sign in twice:
  - The first sign-in starts the regular enrollment process.
  - The second sign-in authenticates the user identity in Company Portal and gets the SSO extension.

  We're working on updates to reduce the number of sign-ins for Platform SSO during Setup Assistant.

When this feature is enabled, users have access to resources immediately when they arrive at desktop.

Prerequisites:

- Before you enroll:
  - Create a [settings catalog policy](../device-configuration/settings-catalog/index.md), and configure the **Enable Registration During Setup** setting and assign to the device via static group. 
  - Deploy the Company Portal (5.2604.0 and newer is required) as a line-of-business app.
- Devices must be enrolled through Apple Business Manager or Apple School Manager using ADE.
- The ADE enrollment profile must be configured to use Setup Assistant with modern authentication and have the **Await final configuration** setting turned on.

> [!div class="checklist"]
> Applies to:
>
> - macOS Automated Device Enrollment (ADE)

### Microsoft Intune will support userless ADE for visionOS and tvOS devices<!-- 29219451 -->

Microsoft Intune will be adding support for userless automated device enrollment (ADE) for visionOS and tvOS devices, enabling you to enroll and manage Apple Vision Pro and Apple TV through Apple Business Manager or Apple School Manager. This capability will support ADE without user affinity and includes custom configuration uploads for settings, default enrollment restrictions, and remote device actions. The feature will be available with Microsoft Intune Plan 2 as part of the Microsoft 365 Suite. Enrolled visionOS and tvOS devices will appear alongside iOS and iPadOS devices in the Intune admin center within **Apple mobile** and can be filtered. Support will require tvOS 26 and later or visionOS 26 and later. We recommend that you keep these devices up to date to receive the latest security fixes.

<!-- *********************************************** -->

## Device management

### Agentic identity for the Policy Configuration Agent (public preview)<!-- 37369520 -->

The Intune Policy Configuration Agent will update to use a Microsoft Entra agentic identity instead of a human user identity. This enables the agent to run policy configuration actions securely and independently.

For existing agents, admins will be able to transition to an agentic identity from the agent's **Settings** tab by selecting **Create new identity**. After the identity is provisioned, the agent will now run on behalf of the logged in user and the information will be scoped by the permissions of that account. For new agents, an agentic identity will be auto provisioned at setup.
 
### Updated minimum version for Intune Management Extension on Windows<!-- 35502983 -->

Windows devices managed by Intune will need to run Intune Management Extension version 1.58.103.0 or later. Devices on earlier versions will no longer receive configurations or updates that depend on the Intune Management Extension, including Win32 app deployments, PowerShell scripts, remediations, and platform scripts.

The Intune Management Extension updates automatically, so most managed devices should already have a compatible version. Verify that your devices can sync with Intune to receive updates.

> [!div class="checklist"]
> Applies to:
>
> - Windows 10/11

### Silence apps on Managed Home Screen to prevent session PIN bypass<!-- 34929486 -->

For devices using Managed Home Screen (MHS), you'll be able to silence apps whenever MHS is prompting the user for authentication, such as during sign-in or at the session PIN screen. When silenced, apps won't be able to start activities, display notifications, appear in recent apps, or trigger toasts, dialogs, or device ringing. You'll be able to configure an allowlist of apps that remain unsilenced during the locked state, ensuring that critical communications like calls aren't interrupted. This feature will be opt-in and configurable, allowing your organization to tailor the experience to its operational needs. Once the device is unlocked, all apps will automatically return to their normal state.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Android Enterprise personally owned devices with a work profile will use Android Management API (AMAPI)<!-- 36840128 -->

When users enroll their personally owned Android devices in Intune, a work profile is created with a separate partition on the device for the user's work account. These devices are referred to as personally owned devices with a work profile.

As part of the Intune move to the [Android Management API](https://developers.google.com/android/management) (opens Android's web site), there will be some updates for personally owned devices that enroll in Intune:

- Web based enrollment for an improved enrollment flow and experience - Users won't have to install an app to enroll in Intune. Web enrollment will be tenant wide.
- New implementation for how Intune delivers policies - Modern update on how Intune delivers and monitors policies on Android personally owned devices with a work profile. This change also aligns with how Intune manages policies on corporate owned devices with a work profile, fully managed, and dedicated devices. You can scale your migration to targeted groups.

To use these features, you will need to opt-in:

- Web based enrollment: **Devices > Device Onboarding > Enrollment > Android > Personally owned devices with a work profile > Use web enrollment for all users enrolling into Android personally-owned work profile management**
- Policy: **Devices > Manage devices > Configuration > Create > New policy > Android Enterprise > Move to Android Management API**

To learn more, see:

- [New policy implementation and web enrollment for Android personally owned work profile blog](https://techcommunity.microsoft.com/blog/intunecustomersuccess/new-policy-implementation-and-web-enrollment-for-android-personally-owned-work-p/4370417)
- [Android Enterprise work profile management overview](../device-enrollment/android/enterprise-work-profile.md)

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise personally owned devices with a work profile

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

The new baseline will be available for [US Government Community Cloud High (GCC High)](../fundamentals/government-service.md) tenants, and focused on audits and not on configuration. Applicable to Windows devices, the baseline generates detailed reports on which devices meet the recommended settings for compliance with STIGs.

> [!div class="checklist"]
> Applies to:
>
> - Windows

For information about the currently available Intune security baselines, see [Security baselines overview](../device-security/security-baselines/overview.md).

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../device-security/microsoft-defender/security-settings-management.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../device-configuration/endpoint-security/attack-surface-reduction.md).

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

### Intune Data Warehouse (beta) connector deprecation in Power BI<!-- 37106409 -->

The Intune Data Warehouse (beta) connector in Power BI will be retired. If you use Power BI reports that rely on this connector, you'll need to transition to Intune connector v2 or the OData Feed connector before the retirement completes.

Power BI reports created after November 2025 already use connector v2. Reports created before November 2025 may still use the beta connector and will need to be updated.

The transition will begin in late April 2026 and occur gradually over two weeks. After the transition completes, data access through the beta connector will no longer be available.

> [!div class="checklist"]
> Applies to:
>
> - Windows
> - iOS/iPadOS
> - macOS
> - Android

### Reporting considerations for compliance policies<!-- 37266708 -->

Intune will add new guidance to the compliance policy reporting documentation to help clarify expected reporting behaviors. This documentation update will address common questions about how compliance policy reports reflect device state, including:

- Check-in dependency: Compliance policy reports are updated when a device checks in with the Intune service. Reporting data refreshes during device check-in and policy refresh cycles and might not immediately reflect recent assignment or targeting changes.
- Multi-user devices: Compliance reports display the compliance state for the last user who checked in on the device. If multiple users sign in to a shared device, the report can reflect the last known compliance state for a previous user.
- Pending status: A device might appear in a **Pending** state if it has not yet checked in to receive or report compliance policy status. This status can persist in reports until the next reporting cycle completes.
- Multiple records: Policy reports can show multiple records for a single device, such as separate entries associated with user and system contexts. This behavior can occur when different users sign in to the same device or when automatic device check-ins occur.
- Summary vs. detail differences: Summary report views and detailed device lists can update on different cadences. As a result, aggregated summary values might temporarily differ from detailed report entries.

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](./includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](index.md).
