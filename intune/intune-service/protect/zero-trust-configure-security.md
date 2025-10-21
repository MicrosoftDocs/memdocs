---
title:  Configure Microsoft Intune for increased security
description:  Learn how to improve your security posture with Microsoft Intune.
ms.topic: reference
ms.date: 10/20/2025
ms.author: brenduns
author: brenduns
ms.reviewer: ramical
ms.collection:
- tier 1
- M365-identity-device-management
---

# Configure Microsoft Intune for increased security (Preview)

The security recommendations in this document are designed to help you improve your organization's security posture by using Microsoft Intune. These recommendations are influenced by accepted industry standards like those developed by NIST, the configuration baselines we use internally at Microsoft, and our experiences with customers. The recommendations in this article for Intune are focused on devices, but guided by the following Microsoft [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars) pillars:

- Protect identities and secrets
- Protect tenants and isolate production systems
- Protect networks
- Protect engineering systems
- Monitor and detect cyberthreats
- Accelerate response and remediation

> [!TIP]
> Some organizations might take these recommendations exactly as written, while others might choose to make modifications based on their own business needs.

We recommend that all of the following controls be implemented where licenses are available. These patterns and practices help to provide a secure foundation for other resources built on top of this solution. More controls will be added to this document over time.

## Secure Tenant

Ensure tenant-level governance, identity, and configuration consistency.

| Check | Minimum License Requirements  |
|-------|-------------------------------|
| [Scope tag configuration is enforced to support delegated administration and least-privilege access](../protect/zero-trust-secure-tenant.md#scope-tag-configuration-is-enforced-to-support-delegated-administration-and-least-privilege-access) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Device enrollment notifications are enforced to ensure user awareness and secure onboarding](../protect/zero-trust-secure-tenant.md#device-enrollment-notifications-are-enforced-to-ensure-user-awareness-and-secure-onboarding) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Windows automatic device enrollment is enforced to eliminate risks from unmanaged endpoints](../protect/zero-trust-secure-tenant.md#windows-automatic-device-enrollment-is-enforced-to-eliminate-risks-from-unmanaged-endpoints) | <ul><li>Microsoft Intune Plan 1</li><li>Microsoft Entra ID P1 *(for Conditional Access)*</li></ul> |
| [Compliance policies protect Windows devices](../protect/zero-trust-secure-tenant.md#compliance-policies-protect-windows-devices) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Compliance policies protect macOS devices](../protect/zero-trust-secure-tenant.md#compliance-policies-protect-macos-devices) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Compliance policies protect fully managed and corporate-owned Android devices](../protect/zero-trust-secure-tenant.md#compliance-policies-protect-fully-managed-and-corporate-owned-android-devices) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Compliance policies protect personally owned Android devices](../protect/zero-trust-secure-tenant.md#compliance-policies-protect-personally-owned-android-devices) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Compliance policies protect iOS/iPadOS devices](../protect/zero-trust-secure-tenant.md#compliance-policies-protect-iosipados-devices) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Device cleanup rules maintain tenant hygiene by hiding inactive devices](../protect/zero-trust-secure-tenant.md#device-cleanup-rules-maintain-tenant-hygiene-by-hiding-inactive-devices) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Terms and Conditions policies protect access to sensitive data](../protect/zero-trust-secure-tenant.md#terms-and-conditions-policies-protect-access-to-sensitive-data) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Company Portal branding and support settings enhance user experience and trust](../protect/zero-trust-secure-tenant.md#company-portal-branding-and-support-settings-enhance-user-experience-and-trust) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Endpoint Analytics is enabled to help identify risks on Windows devices](../protect/zero-trust-secure-tenant.md#endpoint-analytics-is-enabled-to-help-identify-risks-on-windows-devices) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Windows Update policies are enforced to reduce risk from unpatched vulnerabilities](../protect/zero-trust-secure-tenant.md#windows-update-policies-are-enforced-to-reduce-risk-from-unpatched-vulnerabilities) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [Security baselines are applied to Windows devices to strengthen security posture](../protect/zero-trust-secure-tenant.md#security-baselines-are-applied-to-windows-devices-to-strengthen-security-posture) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [Update policies for macOS are enforced to reduce risk from unpatched vulnerabilities](../protect/zero-trust-secure-tenant.md#update-policies-for-macos-are-enforced-to-reduce-risk-from-unpatched-vulnerabilities) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [Update policies for iOS/iPadOS are enforced to reduce risk from unpatched vulnerabilities](../protect/zero-trust-secure-tenant.md#update-policies-for-iosipados-are-enforced-to-reduce-risk-from-unpatched-vulnerabilities) | <ul><li>Microsoft Intune Plan 1</li></ul>  |

For license details, see:

- [Microsoft Intune licensing](../fundamentals/licenses.md)
- [Microsoft Entra licensing](/entra/fundamentals/licensing)

## Secure Devices

Secure endpoints through device configuration and security policies.

| Check | Minimum License Requirements  |
|-------|-------------------------------|
| [Local administrator credentials on Windows are protected by Windows LAPS](../protect/zero-trust-secure-devices.md#local-administrator-credentials-on-windows-are-protected-by-windows-laps) | <ul><li>Microsoft Intune Plan</li></ul> |
| [Local administrator credentials on macOS are protected during enrollment by macOS LAPS](../protect/zero-trust-secure-devices.md#local-administrator-credentials-on-macos-are-protected-during-enrollment-by-macos-laps) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [Local account usage on Windows is restricted to reduce unauthorized access](../protect/zero-trust-secure-devices.md#local-account-usage-on-windows-is-restricted-to-reduce-unauthorized-access) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Data on Windows is protected by BitLocker encryption](../protect/zero-trust-secure-devices.md#data-on-windows-is-protected-by-bitlocker-encryption) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [FileVault encryption protects data on macOS devices](../protect/zero-trust-secure-devices.md#filevault-encryption-protects-data-on-macos-devices) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [Authentication on Windows uses Windows Hello for Business](../protect/zero-trust-secure-devices.md#authentication-on-windows-uses-windows-hello-for-business) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [Attack Surface Reduction rules are applied to Windows devices to prevent exploitation of vulnerable system components](../protect/zero-trust-secure-devices.md#attack-surface-reduction-rules-are-applied-to-windows-devices-to-prevent-exploitation-of-vulnerable-system-components) | <ul><li>Microsoft Intune Plan 1</li><li>Defender for Endpoint Plan 1</li></ul> |
| [Defender Antivirus policies protect Windows devices from malware](../protect/zero-trust-secure-devices.md#defender-antivirus-policies-protect-windows-devices-from-malware) | <ul><li>Microsoft Intune Plan 1</li><li>Defender for Endpoint Plan 1</li></ul>  |
| [Defender Antivirus policies protect macOS devices from malware](../protect/zero-trust-secure-devices.md#defender-antivirus-policies-protect-macos-devices-from-malware) | <ul><li>Microsoft Intune Plan 1</li><li>Defender for Endpoint Plan 1</li></ul>  |
| [Windows Firewall policies protect against unauthorized network access](../protect/zero-trust-secure-devices.md#windows-firewall-policies-protect-against-unauthorized-network-access) | <ul><li>Microsoft Intune Plan 1</li></ul>  |
| [macOS Firewall policies protect against unauthorized network access](../protect/zero-trust-secure-devices.md#macos-firewall-policies-protect-against-unauthorized-network-access) | <ul><li>Microsoft Intune Plan 1</li></ul>  |

For license details, see:

- [Microsoft Intune licensing](../fundamentals/licenses.md)
- [Overview of Microsoft Defender for Endpoint Plan 1](/defender-endpoint/defender-endpoint-plan-1)

## Secure Data

Protect data on devices and in transit, and enforce secure access to organizational data.

| Check | Minimum License Requirements |
|-------|-------------------------------|
| [Data on Android is protected by app protection policies](../protect/zero-trust-secure-data.md#data-on-android-is-protected-by-app-protection-policies) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Data on iOS/iPadOS is protected by app protection policies](../protect/zero-trust-secure-data.md#data-on-iosipados-is-protected-by-app-protection-policies) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Conditional Access policies block access from unmanaged apps](../protect/zero-trust-secure-data.md#conditional-access-policies-block-access-from-unmanaged-apps) | <ul><li>Microsoft Intune Plan 1</li><li>Microsoft Entra ID P1 *(for Conditional Access)*</li></ul> |
| [Conditional Access policies block access from noncompliant devices](../protect/zero-trust-secure-data.md#conditional-access-policies-block-access-from-noncompliant-devices) | <ul><li>Microsoft Intune Plan 1</li><li>Microsoft Entra ID P1 *(for Conditional Access)*</li></ul> |
| [Secure Wi-Fi profiles protect iOS devices from unauthorized network access](../protect/zero-trust-secure-data.md#secure-wi-fi-profiles-protect-ios-devices-from-unauthorized-network-access) | <ul><li>Microsoft Intune Plan 1</li></ul> |
| [Secure Wi-Fi profiles protect Android devices from unauthorized network access](../protect/zero-trust-secure-data.md#secure-wi-fi-profiles-protect-android-devices-from-unauthorized-network-access) | <ul><li>Microsoft Intune Plan 1</li></ul> |

For license details, see:

- [Microsoft Intune licensing](../fundamentals/licenses.md)
- [Microsoft Entra licensing](/entra/fundamentals/licensing)

## Related content

- [Deployment guide for Microsoft Intune](../fundamentals/get-started-with-intune.md)
- [Protect data and devices with Microsoft Intune](../protect/device-protect.md)
- [Configure Microsoft Entra for increased security (Preview)](/entra/fundamentals/configure-security)