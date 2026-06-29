---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
ms.date: 06/29/2026
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

### Agentic identity for the Policy Configuration Agent (public preview)<!-- 37369520 -->

The Intune Policy Configuration Agent will update to use a Microsoft Entra agentic identity instead of a human user identity. This enables the agent to run policy configuration actions securely and independently.

For existing agents, admins will be able to transition to an agentic identity from the agent's **Settings** tab by selecting **Create new identity**. After the identity is provisioned, the agent will now run on behalf of the logged-in user and the information will be scoped by the permissions of that account. For new agents, an agentic identity will be auto provisioned at setup.  

<!-- *********************************************** -->

## Device security

### Audit mode for the Microsoft Defender Antivirus template for Linux<!-- 37284585 -->

We'll soon add a new **Audit** value to the **Enforcement level** setting in the Microsoft Defender Antivirus template for Linux, which is part of Intune's Endpoint Security Antivirus policy. When you set **Enforcement level** to **Audit**, the antivirus engine detects threats in real time but doesn't automatically remediate them. Malware detections are reported as alerts in the Microsoft Defender portal through real-time scanning, without quarantining the malicious files. This gives you visibility into the threat landscape before you turn on full protection.

The Microsoft Defender Antivirus template for Linux is supported for devices [managed by Intune](../device-configuration/endpoint-security/antivirus.md), and for devices managed only by Defender through the [Microsoft Defender for Endpoint security settings management](../device-security/microsoft-defender/security-settings-management.md) scenario (MDE attach).

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

### Custom compliance settings for macOS<!-- 35392462 -->

Microsoft Intune will support custom compliance settings for macOS. You'll be able to define compliance checks using scripts and JSON rules, similar to existing support for Windows and Linux. This capability will allow you to evaluate device configuration, security posture, and other custom attributes not covered by built-in settings. Results will appear alongside standard compliance reporting in the Intune admin center.

> [!div class="checklist"]
> Applies to:
>
> - macOS

### Client-driven compliance evaluation for Windows devices<!-- 37554578 -->

Microsoft Intune will introduce client-driven compliance evaluation for Windows devices to reduce delays in compliance reporting. Supported devices will detect important state changes locally and proactively request a compliance re-evaluation when it matters, instead of waiting for the next scheduled check-in. As an admin, you'll see faster updates for remediation, reporting, and access decisions. This capability will roll out in preview for Windows devices.

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Controlled Configuration for Microsoft Defender antivirus settings<!-- 26715847 -->

Microsoft Intune is bringing Controlled Configuration (CC) to public preview for Microsoft Defender antivirus settings. CC introduces a unified approach to endpoint security by making Intune and Microsoft 365 Defender the single source of truth for antivirus and related security settings.

When you enable CC, all of the Defender antivirus settings that are delivered by Intune or Microsoft Defender for Endpoint security settings management will override configurations from all other channels, including Group Policy, Configuration Manager, and local changes or scripts. This single source of truth will help ensure consistent, predictable device states.

CC extends Tamper Protection by letting you lock settings to admin-defined values, not just defaults. Your Defender antivirus policies set by Intune are reliably enforced across your endpoints, without being overridden by legacy on-premises policies or local per-device changes.

Benefits of CC include:

- **Authoritative policy enforcement**: Cloud-delivered antivirus settings always take precedence, eliminating conflicts from legacy tools.
- **Improved security posture**: Prevents configuration drift and reduces risk from local changes.
- **Simplified troubleshooting**: Clear, predictable configurations make auditing and support easier.

> [!div class="checklist"]
> Applies to:
>
> - Windows

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](./includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](index.md).
