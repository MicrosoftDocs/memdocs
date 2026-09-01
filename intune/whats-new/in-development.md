---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
ms.date: 08/21/2026
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

<!-- ## App management -->

<!-- *********************************************** -->

## Device configuration

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

## Device management

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
