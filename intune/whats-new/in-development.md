---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
ms.date: 05/04/2026
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

## Device configuration

### Disable MAC address randomization on macOS Wi-Fi profiles<!-- 8457343 -->

On macOS devices, the **Disable MAC address randomization** setting will be available for Wi-Fi profiles. You'll be able to use this setting to disable MAC address randomization on managed macOS devices.

When connecting to a network, devices can present a randomized MAC address instead of the physical MAC address. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. But, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

To learn more, see:

- [Wi-Fi profiles settings list](../device-configuration/templates/ref-wifi-settings-apple.md)
- [Learn more about Wi-Fi profiles in Intune](../device-configuration/templates/configure-wifi.md)

> [!div class="checklist"]
> Applies to:
>
> - macOS 15 and later

### New Wired Networks device configuration profile for iOS/iPadOS<!-- 31880672 -->

There will be a new **802.1x Wired Networks** device configuration profile for iOS/iPadOS devices. The feature will support 802.1x Ethernet access controls, which is ideal for M-series iPads that support native resolution screen extension. It will allow iPads to securely connect to hot desk docks and monitors using wired access.

This profile will:

- Support EAP protocols, like TLS, PEAP, and TTLS
- Be similar to the macOS wired network profile experience

This feature will help with secure enterprise deployments for iPads in education, finance, and other regulated industries.

To learn more about wired networks, see [Add and use wired networks settings on your macOS and Windows devices](../device-configuration/templates/configure-wired-networks.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS 17 and newer

### New Block Bluetooth sharing setting in the Android Enterprise settings catalog<!-- 35027842 -->

The [Settings catalog](../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../device-configuration/settings-catalog/index.md).

There will be a new **Block Bluetooth sharing** setting (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type). When set to **True**, the device can't share content over Bluetooth. When set to **False**, fully managed and dedicated devices allow Bluetooth sharing, while corporate-owned work profile devices block Bluetooth sharing.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../device-configuration/settings-catalog/ref-android-settings.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned dedicated devices (COSU)

<!-- *********************************************** -->

## Device enrollment

### Enrollment time grouping for new Apple ADE enrollment policies generally available<!-- 17474465, 28230551 -->

Enrollment time grouping (ETG) will improve the Apple automated device enrollment (ADE) setup experience by providing an efficient way to group devices at enrollment time. The pre-knowledge of the security group that the device will be a member of helps in computing the applicable policies, apps, and settings for the enrolled device, so the configurations are delivered quickly at the time of enrollment.

You'll be able to configure enrollment time grouping in new iOS/iPadOS and macOS enrollment policies that use these authentication methods:

- iOS/iPadOS:
  - Enroll with user affinity
    - Setup Assistant with modern authentication
    - Company Portal authentication method
  - Enroll without user affinity
    - Microsoft Entra shared mode
    - Shared iPad
- macOS:
  - Enroll with user affinity
    - Setup Assistant with modern authentication
  - Enroll without user affinity

There will be a new **Device group** tab within new iOS/iPadOS and macOS enrollment policies where you can add a Microsoft Entra security group. The group you add will map directly to the enrollment profile, and you'll be able to edit the group at any time. The new device grouping tab won't be available in existing enrollment profiles.

Other requirements include adding the Intune first-party app as a security group owner, and ensuring that you have the **enrollment time device membership assignment** permission within a custom RBAC role.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS Automated Device Enrollment (ADE)
> - macOS Automated Device Enrollment (ADE)

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

<!-- *********************************************** -->

## Device management

### Agentic identity for the Policy Configuration Agent (public preview)<!-- 37369520 -->

The Intune Policy Configuration Agent will update to use a Microsoft Entra agentic identity instead of a human user identity. This enables the agent to run policy configuration actions securely and independently.

For existing agents, admins will be able to transition to an agentic identity from the agent's **Settings** tab by selecting **Create new identity**. After the identity is provisioned, the agent will now run on behalf of the logged in user and the information will be scoped by the permissions of that account. For new agents, an agentic identity will be auto provisioned at setup.
 
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

### Improved on-demand sync for Windows devices<!-- 37533252 -->

The Sync device action for Windows devices will be enhanced to trigger a more comprehensive, on-demand synchronization from the Microsoft Intune admin center. Instead of waiting for scheduled check-ins, the sync action will initiate a full synchronization across key workloads, including compliance, configuration policies, apps, and scripts, so devices reflect the latest changes faster.

This improvement will be especially useful during troubleshooting, incident response, or high-priority rollouts where you need faster confirmation that device state matches your intent.

> [!div class="checklist"]
> Applies to:
>
> - Windows

<!-- *********************************************** -->

## Device security

### Strict Tunnel Mode for Microsoft Tunnel on Android<!-- 17373449 -->

Microsoft Tunnel will add support for Strict Tunnel Mode on Android Enterprise devices enrolled through Android Management API (AM API). When Strict Tunnel Mode is enabled, all network traffic is forced through the VPN tunnel. If the VPN connection is unavailable or drops, all network traffic on the device is blocked, preventing apps from accessing the public internet outside of the tunnel. Devices enrolled through the legacy EMM API work profile don't support Strict Tunnel Mode until migrated to AM API.

Admins will be able to configure an app exclusion list. Apps on the exclusion list always bypass the VPN and connect directly to the network, regardless of VPN connection status.

Strict Tunnel Mode will be available as a configuration option when a [Microsoft Tunnel VPN profile](../device-security/microsoft-tunnel/install.md) is configured with **Always On** VPN. For unenrolled devices using [Microsoft Tunnel for Mobile Application Management](../device-security/microsoft-tunnel/mam-android.md), Strict Tunnel Mode will also be supported, blocking network traffic when the MAM Tunnel connection is unavailable.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise personally owned work profile
> - Android Enterprise corporate-owned work profile
> - Android Enterprise corporate-owned fully managed
> - Android (MAM, unenrolled devices)

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

### In-place renewal of Cloud PKI issuing certification authorities (CAs)<!-- 25850620 -->

Currently, Microsoft Intune requires you to create a new Cloud PKI issuing CA and manually update dependent SCEP certificate profiles when an issuing CA nears expiration. This process can increase operational overhead and introduce configuration risk.

Soon, you'll be able to renew eligible Cloud PKI issuing CAs in place. This update will help maintain uninterrupted certificate issuance and support continued certificate-based access for scenarios such as Wi-Fi, VPN, and email, without requiring changes to existing SCEP profiles or device assignments.

> [!div class="checklist"]
> Applies to:
>
> - Cloud PKI

### Custom compliance settings for macOS<!-- 35392462 -->

Microsoft Intune will support custom compliance settings for macOS. You'll be able to define compliance checks using scripts and JSON rules, similar to existing support for Windows and Linux. This capability will allow you to evaluate device configuration, security posture, and other custom attributes not covered by built-in settings. Results will appear alongside standard compliance reporting in the Intune admin center.

> [!div class="checklist"]
> Applies to:
>
> - macOS

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
