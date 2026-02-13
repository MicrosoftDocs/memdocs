---
title: Protect devices with Microsoft Intune
description: Learn about the Intune capabilities that can help you protect your devices and data against unauthorized access and other threats.
author: brenduns
ms.author: brenduns
ms.date: 02/13/2026
ms.topic: overview
ms.reviewer: davidra
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Protect data and devices with Microsoft Intune

Microsoft Intune helps you keep managed devices secure and up to date while protecting your organization's data from compromised devices. Control what users do with organizational data on both managed and unmanaged devices, and block access to data from potentially compromised devices.

This article introduces Intune's built-in security capabilities and partner technologies that work together to support **Zero Trust** solutions for your organization. As an overview, it describes key protection capabilities and links to detailed documentation for configuration and deployment guidance.

## Platform support

From the Microsoft Intune admin center, Intune [supports managed devices](../fundamentals/supported-devices-browsers.md#intune-supported-operating-systems) that run:

- Android
- iOS/iPadOS
- Linux
- macOS
- Windows

**Extend to on-premises devices:**

When you use [Configuration Manager](#configuration-manager) to manage on-premises devices, you can extend Intune policies to those devices through tenant attach or co-management.

## Deploy security policies to protect devices

Deploy policies to configure and enforce security on enrolled devices. The following policy types work together to protect devices:

**[Endpoint security policies](../protect/endpoint-security.md)** - Focused security policies for specific protection areas:
- **Account protection** - Windows Hello for Business, Credential Guard, and Windows LAPS
- **Antivirus** - Microsoft Defender Antivirus configuration and exclusions
- **App Control for Business** - Application allowlisting using Windows Defender Application Control
- **Attack surface reduction** - Reduce exploit vulnerabilities and attack vectors
- **Disk encryption** - BitLocker, Personal Data Encryption (PDE), and FileVault
- **Endpoint detection and response** - Microsoft Defender for Endpoint onboarding
- **Firewall** - Network protection and firewall rules

**[Device configuration policies](../configuration/device-profiles.md)** - Broader device settings including endpoint protection, certificates, software updates, and VPN. Use when you need to combine security settings with device functionality configurations.

**[Device compliance policies](../protect/device-compliance-get-started.md)** - Define device requirements like OS versions, encryption status, and threat levels. Noncompliant devices trigger alerts and can be blocked from organizational resources when combined with [Conditional Access](#conditional-access).

### Key security capabilities

The following security areas can be managed through these policies:

- **Authentication and identity**
  - **Certificates** - Deploy certificates using [SCEP and PKCS profiles](../protect/certificates-configure.md), or use [Microsoft Cloud PKI](../../cloud-pki/index.md) for simplified cloud-based certificate management without on-premises infrastructure. Configure [derived credentials](../protect/derived-credentials.md) for smartcard scenarios.
  - **Modern authentication** - Enable [Windows Hello for Business](../protect/windows-hello.md) for passwordless sign-in. Configure Platform SSO for macOS to strengthen authentication across apps and services.
  - **Multi-factor authentication** - Require MFA and configure PIN/password requirements for enhanced security.

- **Data encryption**
  - **Windows** - Deploy [BitLocker](../protect/encrypt-devices.md) for full disk encryption and [Personal Data Encryption (PDE)](../protect/encrypt-devices.md#personal-data-encryption-pde) for file-level encryption on Windows 11.
  - **macOS** - Manage [FileVault](../protect/encrypt-devices-filevault.md) for full disk encryption.

- **Software updates** - Control when and how devices receive updates:
  - **Android** - [FOTA updates](../../device-updates/android/fota-updates.md) for OEM firmware, [Zebra LifeGuard OTA](../../device-updates/android/zebra-lifeguard-ota-integration.md) for Zebra devices
  - **iOS/iPadOS and macOS** - Manage OS versions and [update schedules](../protect/managed-software-updates-ios-macos.md)
  - **Windows** - Configure [Windows Update behaviors](../../device-updates/windows/index.md), schedule updates, and maintain feature update compliance

- **Application control** - Use [App Control for Business](../protect/endpoint-security-app-control-policy.md) policies to define which applications can run on Windows devices.

- **Attack surface reduction** - Deploy [ASR policies](../protect/endpoint-security-asr-policy.md) to reduce vulnerabilities through exploit protection, device control, application isolation, and ASR rules.

- **Security baselines** - Deploy preconfigured [security baselines](../protect/security-baselines.md) for Windows devices, Microsoft Edge, and Microsoft Defender for Endpoint that reflect Microsoft security team recommendations.

- **Network security**
  - **VPN profiles** - Configure [VPN connections](../configuration/vpn-settings-configure.md#vpn-connection-types) for secure remote access to organizational resources.
  - **Firewall policies** - Manage built-in firewall protection on Windows and macOS devices.

- **Privileged access management**
  - **[Windows LAPS](../protect/windows-laps-overview.md)** - Manage local administrator passwords with automatic rotation and secure backup to Active Directory or Microsoft Entra.
  - **[Endpoint Privilege Management](#add-endpoint-privilege-management)** - Run users as standard accounts while allowing elevation for approved applications.

## Protect data with app protection policies

Protect organizational data at the application layer using [app protection policies](../apps/app-protection-policy.md) with Intune-managed apps. These protections work on both enrolled and unenrolled devices, supporting Bring Your Own Device (BYOD) scenarios.

**Intune-managed apps** integrate the [Intune App SDK](../developer/app-sdk.md) or use the [Intune App Wrapping Tool](../developer/apps-prepare-mobile-application-management.md). See [Intune protected apps](../apps/apps-supported-intune-apps.md) for a list of supported apps. Users can access organizational data only through managed apps when app protection policies are enforced, while personal data remains unaffected.

**Key app protection policy capabilities:**

- Require PIN or biometric authentication for organizational data access
- Block copy/paste, screenshots, and data transfer to unmanaged apps
- Prevent saving organizational data to personal storage
- Enforce encryption of organizational data at rest
- Wipe organizational data remotely when devices are lost or users leave

## Use device actions to protect devices and data

Run immediate [device actions](../remote-actions/index.md) to respond to security incidents or maintain device security. Unlike policies that maintain ongoing configurations, device actions execute once when invoked. Actions take effect immediately for online devices, or at next check-in for offline devices. [Bulk device actions](../remote-actions/index.md#bulk-device-actions) can target multiple devices simultaneously.

**Common security actions:**

- **Remote lock** - Lock a device remotely to prevent unauthorized access
- **Wipe** - Factory reset a device, removing all data and settings
- **Retire** - Remove organizational data while preserving personal data
- **BitLocker key rotation** (Windows) - Rotate encryption keys for enhanced security
- **Antivirus scan** (Windows) - Run full or quick malware scans
- **Update Defender intelligence** - Refresh threat definitions
- **Disable Activation Lock** (iOS/iPadOS) - Remove Activation Lock for device reuse

These actions are also available for [co-managed devices](#configuration-manager) managed by Configuration Manager with tenant attach.

## Integrate with partner technologies

Extend Intune's protection capabilities through integrations with Microsoft technologies and third-party partners.

### Compliance partners

Integrate [device compliance data](../protect/device-compliance-partners.md) from third-party MDM solutions with Microsoft Entra ID. Conditional Access policies can then enforce access controls using compliance status from multiple sources.

### Configuration Manager

Extend Intune security policies to Configuration Manager devices using [co-management](../../configmgr/comanage/overview.md) or [tenant attach](../../configmgr/tenant-attach/device-sync-actions.md):

- **Co-management** - Manage Windows devices with both Configuration Manager and Intune simultaneously
- **Tenant attach** - Synchronize Configuration Manager devices to Intune for centralized management

Once integrated, [apply Intune security policies](../protect/endpoint-security-manage-devices.md) including endpoint security policies, compliance policies, certificates (SCEP/PKCS), and security baselines to Configuration Manager devices.

### Mobile Threat Defense

[Mobile Threat Defense (MTD)](../protect/mobile-threat-defense.md) apps scan devices for threats and report risk levels to Intune. Use MTD threat levels in compliance policies, app protection policies, and Conditional Access to block compromised devices from accessing organizational resources.

**MTD capabilities for [enrolled devices](../protect/mtd-device-compliance-policy-create.md):**
- Deploy and manage MTD apps through Intune
- Use threat levels in compliance and Conditional Access policies
- Block or allow data access based on device risk

**MTD capabilities for [unenrolled devices](../protect/mtd-app-protection-policy.md):**
- Use threat levels in app protection policies
- Block access to organizational data on high-risk devices

**Supported MTD solutions:**
- [Microsoft Defender for Endpoint](../protect/microsoft-defender-with-intune.md) with enhanced Intune integration
- [Third-party MTD partners](../protect/mobile-threat-defense.md#mobile-threat-defense-partners)

### Microsoft Defender for Endpoint

[Microsoft Defender for Endpoint integrates with Intune](../protect/microsoft-defender-with-intune.md) across Windows, macOS, Linux, Android, and iOS/iPadOS to provide:

- **Mobile Threat Defense** - Device risk assessment for compliance and Conditional Access policies
- **[Microsoft Tunnel](../protect/microsoft-tunnel-overview.md)** - VPN gateway for Intune using Defender for Endpoint as the client app on Android
- **[Security tasks](../protect/atp-manage-vulnerabilities.md)** - Vulnerability management collaboration between Defender for Endpoint and Intune teams
- **Enhanced security policies** - Additional capabilities for [Antivirus](../protect/endpoint-security-antivirus-policy.md) and [Endpoint detection and response (EDR)](../protect/endpoint-security-edr-policy.md) policies

### Conditional Access

[Conditional Access](../protect/conditional-access.md) is a Microsoft Entra capability that enforces access controls based on device compliance and threat levels reported by Intune.

**Conditional Access with Intune:**

- **[Device-based](../protect/create-conditional-access-intune.md)** - Require devices to be compliant before accessing organizational resources
- **[App-based](../protect/app-based-conditional-access-intune.md)** - Ensure only apps with Intune app protection policies can access Microsoft 365 services

**Conditional Access works with:**
- Device compliance policies
- Microsoft Defender for Endpoint and MTD apps
- Device compliance partners
- App protection policies

## Add Endpoint Privilege Management

[Endpoint Privilege Management (EPM)](../protect/epm-overview.md) enforces **least privilege access** for Windows users by running them as standard users while allowing temporary elevation for approved applications. This Zero Trust approach reduces attack surface by preventing blanket administrative access.

**How EPM works:**

- Users run as standard accounts by default
- Elevation rules define which applications can run with elevated privileges
- Applications are validated using file hashes, certificates, or other criteria
- Common elevated scenarios: application installations, driver updates, Windows diagnostics

> [!TIP]
> EPM is available as an [Intune add-on](../fundamentals/intune-add-ons.md) for Windows devices and requires an additional license.

## Next steps

Build your Zero Trust security posture with Intune:

- **Plan your approach** - Review [Zero Trust security guidance](../protect/zero-trust-configure-security.md) for Intune
- **Configure endpoint security** - Start with [endpoint security policies](../protect/endpoint-security.md) for focused security configurations
- **Implement compliance** - Deploy [device compliance policies](../protect/device-compliance-get-started.md) and [Conditional Access](../protect/conditional-access.md)
- **Protect data** - Configure [app protection policies](../apps/app-protection-policy.md) for organizational data
- **Monitor and maintain** - Learn about [data security and sharing in Intune](../protect/privacy-data-secure-share.md)
