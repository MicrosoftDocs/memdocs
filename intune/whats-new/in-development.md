---
title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
ms.date: 06/11/2026
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

## App management

### Auto-update for Enterprise App Management applications <!-- 33727305  -->

You'll be able to automatically keep Enterprise App Management (EAM) applications up to date using Microsoft Intune. When you enable auto-update for an EAM app with a required assignment, Intune will detect when a newer version is available in the EAM catalog and automatically update the app on targeted devices.

Auto-update for EAM apps will help you:

- Simplify app lifecycle management by eliminating manual packaging and supersedence workflows.
- Reduce operational overhead at scale by removing the long tail of update maintenance.
- Keep devices secure with reliable, timely application updates.

> [!div class="checklist"]
> Applies to:
>
> - Windows  

### Enterprise App Management support for GCC High and DoD<!-- 24875296 -->

Enterprise App Management (EAM) in Microsoft Intune will extend to GCC High (GCCH) and DoD cloud environments. Government customers will be able to use the EAM enterprise catalog to discover, deploy, and keep prepackaged Microsoft and third-party apps up to date without manual repackaging. EAM in sovereign clouds uses a secure cross-cloud integration model that maintains the compliance boundaries and authentication requirements expected for government tenants. This brings cloud-native app management, including faster deployment and reduced packaging overhead, to GCCH and DoD organizations.

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Multiple managed accounts for app protection policies <!-- 3182632 -->

The Multiple Managed Accounts (MMA) feature for Intune mobile application management (MAM) will enable users to add and manage more than one managed account within a single app. With MMA, app protection policies will be enforced independently for each account, as defined by the admin. This capability will be especially useful for scenarios such as consultants working across organizations, company acquisitions, or users managing multiple mailboxes within the same tenant.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - Android

<!-- *********************************************** -->

## Device configuration

### New Android Enterprise settings in the Intune settings catalog<!-- 24964827, 24964854, 24964861, 24964848, 33982123, 33982122, 33982129, 33982130, 33982131, 33982127, 30798336, 37087237, 24964874, 24964888, 33982120, 31576322, 32195504, 35028596 -->

The settings catalog lists all the settings you can configure in a device policy, and all in one place. The following new Android Enterprise settings are available in the Microsoft Intune settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type).

#### Communication and calling

| Setting | Description | Applies to |
|---|---|---|
| <!-- 24964827 --> **Block cell broadcast** | When set to **True**, the device is prevented from receiving cell broadcast messages, such as emergency alerts. When set to **False** (default), Intune doesn't change or update this setting, and the OS might allow the reception of cell broadcast messages. | COBO, COSU, and COPE |
| <!-- 24964854 --> **Block SMS** | When set to **True**, the device is prevented from sending or receiving SMS messages, restricting text communication. When set to **False** (default), the device follows the default SMS behavior of the OS. | COBO, COSU, and COPE |
| <!-- 24964861 --> **Block outgoing calls** | When set to **True**, users are prevented from making outgoing calls on the device. When set to **False** (default), Intune doesn't change or update this setting, and the OS might allow outgoing calls. | COBO, COSU, and COPE |

#### Connectivity and networking

| Setting | Description | Applies to |
|---|---|---|
| <!-- 24964848 --> **Block mobile networks configuration** | **True** prevents users from configuring or modifying mobile network settings on the device. When set to **False** (default), Intune doesn't change or update this setting, and the OS might allow users to adjust mobile network settings. | COBO, COSU, and COPE |
| <!-- 33982123 --> **Block configuring VPN** | When set to **True**, users can't add, edit, or remove VPN configurations on the device. When set to **False** or not configured, the device follows the default VPN configuration behavior of the OS. Found in the **Connectivity** category. To configure, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**, choose **Android Enterprise** as the platform, select the corporate-owned device type, and choose **Settings catalog** as the profile type. Search for **Block configuring VPN** and add it to your policy. | COBO, COSU, and COPE |
| <!-- 33982122 --> **Block network reset** | When set to **True**, the device won't reset network settings even if a reset is attempted. When set to **False** (default), the device follows the default network reset behavior of the OS. | COBO, COSU, and COPE |
| <!-- 33982129 --> **Block airplane mode** | When set to **True**, the device is prevented from enabling airplane mode. When set to **False**, the device follows the default airplane mode behavior of the OS. | COBO, COSU, and COPE |
| <!-- 33982130 --> **Block ultra wideband** | When set to **True**, the device prevents ultra wideband functionality, restricting user access to the setting. When set to **False** (default), the device follows the default ultra wideband behavior of the OS. Supported on Android 14 and above. | COBO, COSU, and COPE |
| <!-- 33982131 --> **Block cellular 2G** | When set to **True**, the device prevents cellular 2G functionality, restricting user access to the setting. When set to **False** (default), the device follows the default cellular 2G behavior of the OS. Supported on Android 14 and above. | COBO, COSU, and COPE |
| <!-- 33982127 --> **Select minimum Wi-Fi security level** | Select the minimum Wi-Fi security level required for the device to connect to Wi-Fi networks. Options are **Open network security**, **Personal network security**, **Enterprise network security**, and **Enterprise 192-bit network security**. The default is **Open network security**, which allows the device to connect to all types of Wi-Fi networks. Supported on Android 13 and later. | COBO, COSU, and COPE |
| <!-- 30798336 --> **Allow selection of a preferential network service** | When set to **True**, the device gives priority to the specified network service over other available options, such as an enterprise slice on 5G networks. When set to **False**, the device connects using its default network selection process. | COBO, COSU, and COPE |

#### eSIM management

| Setting | Description | Applies to |
|---|---|---|
| <!-- 37087237 --> **Block users from adding eSIM profiles** | When set to **True**, users can't add eSIM profiles to the device. When set to **False** (default), users can add eSIM profiles based on the default behavior of the OS. | COBO, COSU, and COPE |

#### Device personalization and display

| Setting | Description | Applies to |
|---|---|---|
| <!-- 24964874 --> **Block wallpaper changes** | When set to **True**, users are prevented from changing the wallpaper on the device. When set to **False** (default), Intune doesn't change or update this setting, and the OS might allow users to change the wallpaper. | COBO, COSU, and COPE |
| <!-- 24964888 --> **Block user icon changes** | When set to **True**, users are prevented from changing their user icon or profile image on the device. When set to **False** (default), Intune doesn't change or update this setting, and the OS might allow users to modify their user icon. | COBO, COSU, and COPE |

#### Printing

| Setting | Description | Applies to |
|---|---|---|
| <!-- 33982120 --> **Block printing** | When set to **True**, the device is prevented from printing documents. When set to **False** (default), the device follows the default printing behavior of the OS. | COBO, COSU, and COPE |

#### Security and work profile

| Setting | Description | Applies to |
|---|---|---|
| <!-- 31576322 --> **Block one lock for device and work profile** | When set to **True**, forces users to use two different passwords for their lock screen and work profile. When set to **False**, Intune doesn't change or update this setting. By default, the OS might allow users to have the same password. | COPE |
| <!-- 32195504 --> **Allow widgets from work profile apps** | When set to **True**, allows users to access widgets exposed by apps in the work profile on the device's home screen. When set to **False**, prevents access to these widgets. By default, the OS might allow widget access. | COPE |
| <!-- 35028596 --> **Block apps from exposing app functions** | This setting controls whether managed apps can expose app functions (programmatic actions that other apps and on-device assistants or AI agents can invoke inside the app). When set to **True**, apps on fully managed devices and apps in the work profile on corporate-owned devices are blocked from exposing app functions. When set to **False** (default OS behavior), apps are allowed to expose app functions. | COBO, COSU, and COPE |

**Platform key:**

- **COBO**: Android Enterprise corporate-owned fully managed
- **COSU**: Android Enterprise corporate-owned dedicated devices
- **COPE**: Android Enterprise corporate-owned devices with a work profile (at work profile level)

For a list of all settings you can currently configure, see [Android Enterprise device settings list in the Intune settings catalog](../device-configuration/settings-catalog/ref-android-settings.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

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

### Support for WPA3-Personal in iOS/iPadOS Wi-Fi profiles<!-- 36602689 -->

Microsoft Intune will support **WPA3-Personal** as a security-type option when configuring Wi-Fi device configuration profiles for iOS/iPadOS. Admins will be able to select WPA3-Personal alongside existing options such as WPA2-Personal.

This feature:

- Allows managed iOS/iPadOS devices to connect to networks that require the stronger WPA3 protocol.
- Brings iOS/iPadOS in line with the latest Wi-Fi Alliance security standards and helps organizations meet evolving network-security requirements.

Support for WPA3 on Windows, Android, and macOS platforms and for WPA3-Enterprise will be available in a future release (no ETA).

To learn more about the settings you can currently configure, see [Add Wi-Fi settings to Apple devices in Microsoft Intune](../device-configuration/templates/ref-wifi-settings-apple.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS  

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

<!-- *********************************************** -->

## Device management

### Remote Help support for RemoteApp in Azure Virtual Desktop<!-- 33047374 -->  

Remote Help will support RemoteApp in Azure Virtual Desktop (AVD), enabling help desk agents to securely view and control apps running within RemoteApp sessions.  

### Agentic identity for the Policy Configuration Agent (public preview)<!-- 37369520 -->

The Intune Policy Configuration Agent will update to use a Microsoft Entra agentic identity instead of a human user identity. This enables the agent to run policy configuration actions securely and independently.

For existing agents, admins will be able to transition to an agentic identity from the agent's **Settings** tab by selecting **Create new identity**. After the identity is provisioned, the agent will now run on behalf of the logged-in user and the information will be scoped by the permissions of that account. For new agents, an agentic identity will be auto provisioned at setup.

### Android Enterprise personally owned devices with a work profile will use Android Management API (AMAPI)<!-- 36840128 -->

When users enroll their personally owned Android devices in Intune, a work profile is created with a separate partition on the device for the user's work account. These devices are referred to as personally owned devices with a work profile.

As part of the Intune move to the [Android Management API](https://developers.google.com/android/management) (opens Android's web site), there will be some updates for personally owned devices that enroll in Intune:

- Web based enrollment for an improved enrollment flow and experience - Users won't have to install an app to enroll in Intune. Web enrollment will be tenant wide.
- New implementation for how Intune delivers policies - Modern update on how Intune delivers and monitors policies on Android personally owned devices with a work profile. This change also aligns with how Intune manages policies on corporate owned devices with a work profile, fully managed, and dedicated devices. You can scale your migration to targeted groups.

To use these features, you will need to opt in:

- Web based enrollment: **Devices > Device Onboarding > Enrollment > Android > Personally owned devices with a work profile > Use web enrollment for all users enrolling into Android personally-owned work profile management**
- Policy: **Devices > Manage devices > Configuration > Create > New policy > Android Enterprise > Move to Android Management API**

To learn more, see:

- [New policy implementation and web enrollment for Android personally owned work profile blog](https://techcommunity.microsoft.com/blog/intunecustomersuccess/new-policy-implementation-and-web-enrollment-for-android-personally-owned-work-p/4370417)
- [Android Enterprise work profile management overview](../device-enrollment/android/enterprise-work-profile.md)

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise personally owned devices with a work profile

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

### Updated security baseline for Microsoft 365 Apps for Enterprise<!-- 35894711 -->

An updated security baseline for **Microsoft 365 Apps for Enterprise** will be available in Microsoft Intune. This baseline aligns with the most recent Microsoft 365 Apps security guidance and includes updated policy recommendations to help protect against evolving threats.

This new baseline will be version **v2512**, skipping the previously published version found in the Security Compliance Toolkit (v2412). Once available, review the new baseline carefully before adopting it.

The following three settings won't be available in this baseline release and are expected to be added in a future update. However, the parent setting to these three, (**VBA Macro Notification Settings** set to *Disable all except digitally signed macros*) will continue to be included in the 2512 update:

- **Require macros to be signed by a trusted publisher**: Pending availability in the Settings Catalog.
- **Block certificates originating from the current user store only**: Pending availability in the Settings Catalog.
- **Require Extended Key Usage (EKU) for code signing**: Pending availability in the Settings Catalog.

Existing profiles won't automatically upgrade. To use the latest version, [create a new baseline profile](../device-security/security-baselines/configure-baselines.md#create-a-profile-for-a-security-baseline) or [update an existing profile to the latest version](../device-security/security-baselines/configure-baselines.md#update-a-baseline-profile-to-the-latest-version).

For a detailed breakdown of setting changes, see the blog post [Security baseline for M365 Apps for enterprise v2512](https://techcommunity.microsoft.com/blog/Microsoft-Security-Baselines/security-baseline-for-m365-apps-for-enterprise-v2512/4487213).

> [!div class="checklist"]
> Applies to:
>
> - Windows

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
