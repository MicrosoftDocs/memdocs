---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
ms.date: 09/01/2026
ms.topic: whats-new
ai-usage: ai-assisted
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

We're fixing how scope tags work with Endpoint Privilege Management (EPM) reports. With this change, EPM reports will respect the report viewer's assigned scope and display the details for only the users and devices that the report user is scoped to view.  

<!-- ***********************************************-->

## App management

### Require Managed Home Screen authentication for protected app activities<!-- 35765469 -->

For Android Enterprise dedicated devices using Managed Home Screen (MHS) with Microsoft Entra shared device mode, Intune will allow admins to requiring users to complete MHS authentication state before allowing protected activities in MAM-integrated apps. When MHS requires sign-in or session PIN authentication, users will still be able to complete limited actions, such as accepting or declining incoming calls. If a user tries to open another protected activity, the app will return them to MHS to authenticate. After authentication, protected app activities will become available normally. This behavior will help prevent users from bypassing the MHS session PIN while preserving critical communication actions.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned dedicated devices using Managed Home Screen with Microsoft Entra shared device mode

### Declarative VPP app download in Company Portal<!-- 30483698 -->

The iOS/iPadOS Company Portal will support Declarative Volume-Purchased Program (VPP) app downloads from the Apps tab. Declarative VPP apps provide an improved end-user experience by reducing app installation latency, allowing for automatic overnight app updates, and providing the end user with a live status of an app installation. If you choose not to use Declarative VPP apps, there will be no changes to the admin and user experience.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### New Apple settings in the Settings Catalog for iOS/iPadOS and macOS<!-- 39430305 -->

Microsoft Intune will add new Apple settings for supported iOS/iPadOS and macOS devices. You'll be able to configure the new options by using Settings Catalog profiles in the Microsoft Intune admin center. These settings will expand the device management controls available through Intune and help you manage Apple devices with a consistent policy workflow. To see these settings, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Enforce Routes capability in iOS/iPadOS and macOS VPN profiles<!-- 28869584 -->

Microsoft Intune will support Apple's **[Enforce Routes](https://developer.apple.com/documentation/networkextension/nevpnprotocol/enforceroutes)** feature in iOS/iPadOS and macOS VPN profiles.

This feature helps prevent situations where VPN traffic accidentally or maliciously goes outside the VPN tunnel, like what happens with de-cloaking risks. It ensures VPN routing aligns with Apple's platform semantics.

When you configure this feature in Intune, routing behavior is defined using **Include all networks** and **Exclude local networks** settings. Intune automatically derives the appropriate **Enforce Routes** configuration based on these selections to ensure consistent and predictable device behavior.

To learn more about VPN profiles in Intune, see:

- [Create VPN profiles to connect to VPN servers in Intune](../device-configuration/templates/configure-vpn.md)
- [Add VPN settings to Apple devices in Microsoft Intune](../device-configuration/templates/ref-vpn-settings-apple.md)

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Disable MAC address randomization on macOS Wi-Fi profiles<!-- 8457343 -->

On macOS devices, the **Disable MAC address randomization** setting will be available for Wi-Fi profiles. Use this setting to disable MAC address randomization on managed macOS devices.

When connecting to a network, devices can present a randomized MAC address instead of the physical MAC address. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. However, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

For more information, see:

- [Wi-Fi profile settings for Apple devices](../device-configuration/templates/ref-wifi-settings-apple.md)
- [Add and use Wi-Fi settings on your devices in Microsoft Intune](../device-configuration/templates/configure-wifi.md)

> [!div class="checklist"]
> Applies to:
>
> - macOS 15 and later

<!-- *********************************************** -->  

<!-- *********************************************** -->

## Device enrollment

### Automatically launch Microsoft Defender for Endpoint during Android Enterprise device setup<!-- 38079776 -->

You'll be able to configure Microsoft Defender for Endpoint to open automatically during out-of-box setup for supported corporate-owned Android Enterprise devices. After you configure the Defender for Endpoint connector, turn on **Grant MTD role permissions**, and assign the Defender app as required, you'll enable this experience from **Endpoint security** > **Defender for Endpoint**. Intune will open Defender during enrollment so users can complete its initial configuration as part of device setup. If configuration isn't completed, the Intune setup step will remain available so users can open Defender again. This experience will help ensure that Defender is configured before enrollment finishes.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned fully managed devices (COBO)
> - Android Enterprise corporate-owned devices with a work profile (COPE)

<!-- *********************************************** -->

## Device management

### Updated minimum supported version for macOS<!-- 38259939 -->

Microsoft Intune will update its minimum supported macOS version after Apple releases macOS 27. Intune, the Company Portal, and the Intune management agent will support macOS 15 and later. Devices running macOS 14 or earlier that are already enrolled will remain enrolled, but new devices on those versions won't be able to enroll. You'll be able to use Intune reporting to identify affected devices and plan upgrades. Devices enrolled without user affinity have a separate support statement.

> [!div class="checklist"]
> Applies to:
>
> - macOS

### Updated minimum supported version for iOS and iPadOS<!-- 38546204 -->

Microsoft Intune will update its minimum supported operating-system version after Apple releases iOS and iPadOS 27. Intune device management, the Company Portal, and app protection policies will require iOS/iPadOS 18 or later for standard supported scenarios. You'll be able to use Intune reports to identify affected devices and users and plan operating-system upgrades before the change. Userless devices enrolled through Automated Device Enrollment have a separate support statement and should be evaluated using the applicable guidance.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

### New single device page becomes the default experience in the Intune admin center<!-- 16532161 -->

Starting with Intune's September (2609) release, the new single device page in the Intune admin center will become the default experience for all admins, and the previous device page will no longer be available. When you go to **Devices** > **All devices** and select a device, you'll use a consolidated view to find device details and properties, monitor activity, access tools and reports, and perform device actions. A consistent layout across platforms will group actions by purpose and show only supported and permitted actions, helping you find information and complete common device-management tasks more efficiently. Existing device-management capabilities will remain available in the redesigned experience.

> [!div class="checklist"]
> Applies to:
>
> - All platforms

### Stage app and policy rollout with deployment plans<!-- 33144262 -->

Deployments and Deployments plans will give you a new way to roll out apps and configuration policies in Intune. Instead of assigning to all targeted groups at once, you'll be able to stage a rollout across multiple rings, control the timing of each ring, and monitor progress from a new **Deployments** experience in the Intune admin center. Plans provide reusable templates that define standardized rollout patterns for delivering a payload across devices in controlled stages, or rings. Deployments integrate with Multiple Admin Approval for change control. This helps you reduce risk when introducing changes to large device fleets.

> [!div class="checklist"]
> Applies to:
>
> - Windows
> - Win32 and Enterprise app catalog apps
> - Settings catalog and Endpoint security policies

### Bulk eSIM activation and wipe options for corporate-owned Android Enterprise devices<!-- 39365748 -->

You'll be able to use Microsoft Intune bulk device actions to activate eSIMs on up to 100 supported corporate-owned Android Enterprise devices running Android 15 or later by using a carrier activation server URL. When you bulk wipe supported devices, Intune will preserve eSIM data plans by default, and you'll be able to choose to remove them when needed. These bulk actions will help you deploy or retire devices more efficiently without configuring each device individually. Personally owned Android Enterprise work profile devices won't be supported.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned fully managed devices (COBO)
> - Android Enterprise corporate-owned dedicated devices (COSU)
> - Android Enterprise corporate-owned devices with a work profile (COPE)

### Device query for multiple devices for app inventory on Windows<!-- 25850932 -->

Advanced Analytics will extend device query for multiple devices to cover app inventory data on Windows. Building on the existing multi-device query for hardware inventory, you'll be able to use Kusto Query Language (KQL) to investigate installed applications across your entire Windows fleet—identifying versions, surfacing outdated or unwanted software, and producing detailed reports without targeting devices one at a time. Multi-device app inventory queries will run against collected inventory data, so you get fleet-wide answers for compliance reviews, vulnerability triage, and license-tracking scenarios.

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Agentic identity for the Policy Configuration Agent (public preview)<!-- 37369520 -->

The Intune Policy Configuration Agent will update to use a Microsoft Entra agentic identity instead of a human user identity. This enables the agent to run policy configuration actions securely and independently.

For existing agents, admins will be able to transition to an agentic identity from the agent's **Settings** tab by selecting **Create new identity**. After the identity is provisioned, the agent will now run on behalf of the logged-in user and the information will be scoped by the permissions of that account. For new agents, an agentic identity will be auto provisioned at setup.  

<!-- *********************************************** -->

## Device security

### Configure Quality Update approvals and policies for Quick Machine Recovery (QMR)<!-- 33856442, 32995296 -->

Windows Autopatch currently offers limited control over the deployment of quality updates. Today, the *expedite mechanism* focuses on deploying the latest security update and doesn't let admins select specific quality update releases or apply different deployment schedules, which can limit compliance, validation, and operational planning scenarios.

Soon, Windows Autopatch will let you explicitly approve, auto-approve, reject, and schedule quality updates by update type, using the same approval infrastructure used for driver updates. This unified model helps you control what content is deployed and when, so you can align rollout timing with testing, compliance, and business readiness requirements. You'll be able to independently manage:

- Monthly security updates
- Monthly non-security updates
- Out-of-band security updates
- Out-of-band non-security updates

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Associate devices to your organization with Windows Autopilot device preparation<!-- 17307894 -->

A new capability for Windows Autopilot device preparation will be available soon: *device association*. Device association binds a Windows device to your organization and enables advanced functionality such as streamlined out-of-box experience (OOBE) pages, device naming before enrollment, and device-based targeting. It also improves onboarding security by verifying device identity before enrollment through hardware-based attestation and TPM-backed cryptographic validation, helping ensure that only trusted devices can access organizational resources.

> [!div class="checklist"]
> Applies to:
>
> - Windows

### New Linux antivirus settings for Microsoft Defender for Endpoint<!-- 37379884 -->

We're adding a new Microsoft Defender Updates template for Linux endpoint security antivirus policies. This template will include four new settings for managing Microsoft Defender for Endpoint agent auto-update behavior on Linux devices attached via MDE attach. You will be able to configure update channels and scheduling for Defender engine, platform, and security intelligence updates.

> [!div class="checklist"]
> Applies to:
>
> - Linux

### Mark Windows devices noncompliant when prohibited AI agents are discovered<!-- 37387056 -->

Automatically mark Windows devices as noncompliant when prohibited local AI agents, such as OpenClaw, are discovered on the device. As an admin, you'll be able to configure a list of prohibited agents in a Windows compliance policy. When a prohibited agent is detected, the device reports as noncompliant and Conditional Access takes effect. The device returns to a compliant state once the agent is removed.

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../device-security/microsoft-defender/security-settings-management.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../device-configuration/endpoint-security/attack-surface-reduction.md).

> [!div class="checklist"]
> Applies to the following when you use the *Windows* platform:
>
> - Windows 10
> - Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

### Client-driven compliance evaluation for Windows devices<!-- 37554578 -->

Microsoft Intune will introduce client-driven compliance evaluation for Windows devices to reduce delays in compliance reporting. Supported devices will detect important state changes locally and proactively request a compliance re-evaluation when it matters, instead of waiting for the next scheduled check-in. As an admin, you'll see faster updates for remediation, reporting, and access decisions. This capability will roll out in preview for Windows devices.

> [!div class="checklist"]
> Applies to:
>
> - Windows

<!-- *********************************************** -->

## Monitor and troubleshoot

### Remote Help support in GCCH<!-- 23122683 -->

You'll be able to use Remote Help in US Government Community Cloud High (GCCH) environments. This expansion extends the same secure, cloud-based remote assistance capabilities currently available in GCC to GCCH tenants. IT support staff will be able to establish Remote Help sessions with end users on GCCH-enrolled devices, providing real-time troubleshooting with role-based access controls through Intune. Both helpers and sharers must sign in with their organization's Microsoft Entra ID accounts.

> [!div class="checklist"]
> Applies to:
>
> - Android
> - macOS
> - Windows

### Certificate connector health monitoring in the Microsoft Intune admin center<!-- 37746972 -->

The Certificate Connector for Microsoft Intune will surface new health and status signals in the admin center, so you can spot certificate-issuance problems early. You'll get clear indicators for common failure conditions — such as the connector being unable to reach the certification authority (CA), the connector's service account lacking permission to issue or revoke certificates, or certificate requests being rejected because of a template mismatch with your SCEP or PKCS profile. Each signal includes guidance to help you investigate and remediate before devices relying on certificate-based authentication hit access, sign-in, or compliance issues.

> [!div class="checklist"]
> Applies to:
>
> - Certificate Connector for Microsoft Intune

<!-- *********************************************** -->

## Role-based access control

### Scoped permissions for role-based access control moving to general availability<!-- 27067241 -->

The **Scoped permissions** setting for role-based access control (RBAC) will move from public preview to general availability. Scoped permissions prevents Intune from merging permissions across multiple role assignments that share the same permission category but use different scope tags. When enabled, each role assignment's permissions apply only within its own scope tag context, giving admins exactly the access you intended.

When this feature reaches general availability, Scoped permissions will become the default behavior for all tenants.

If you haven't enabled Scoped permissions yet, use the **Permissions Assessment Report** at **Tenant administration** > **Roles** > **Settings** to preview how permissions will change before opting in.

For more information, see [Permission behavior across role assignments](../fundamentals/role-based-access-control/scope-tags.md#permission-behavior-across-role-assignments).

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](./includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](index.md).
