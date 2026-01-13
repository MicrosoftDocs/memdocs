---
title: Integrate Microsoft Defender for Endpoint with Intune for Device Compliance
description: Integrate Microsoft Defender for Endpoint with Microsoft Intune as a Mobile Threat Defense (MTD) solution to enforce device compliance and prevent security breaches.
author: brenduns
ms.author: brenduns
ms.date: 01/13/2026
ms.topic: article
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- highpri
- sub-secure-endpoints
---

# Integrate Microsoft Defender for Endpoint with Intune for Device Compliance

Learn how integrating Microsoft Defender for Endpoint with Microsoft Intune can protect your organization. This integration lets you assess device risk in real time and automatically block compromised devices from corporate resources to prevent security breaches and limit their impact by automatically marking risky devices as noncompliant.

For example, if malware compromises a user's device, Microsoft Defender for Endpoint flags that device as high-risk and Intune can automatically cut off its access to corporate resources.

> [!TIP]
> Before you begin, ensure your account is assigned an Intune role with sufficient permissions to configure these settings. For example, the built-in [Endpoint Security Manager](../undamentals/role-based-access-control#built-in-roles) role has the necessary permissions.

## Integration workflow

The following workflow applies to devices enrolled with Intune. For detailed instructions, see [Configure Microsoft Defender for Endpoint in Intune](../protect/microsoft-defender-integrate.md):

1. [Establish a service-to-service connection](../protect/microsoft-defender-integrate.md#connect-microsoft-defender-for-endpoint-to-intune) between Intune and Microsoft Defender for Endpoint.
2. [Onboard devices](../protect/microsoft-defender-integrate.md#onboard-devices) with Microsoft Defender for Endpoint using Intune policy.
3. [Create a device compliance policy](../protect/microsoft-defender-integrate.md#create-and-assign-compliance-policy-to-set-device-risk-level) to set acceptable risk levels.
4. [Configure Conditional Access policy](../protect/microsoft-defender-integrate.md#create-a-conditional-access-policy) to block noncompliant devices.

**Extend the integration:** Once configured, you can [leverage Threat & Vulnerability Management (TVM)](atp-manage-vulnerabilities.md) to remediate endpoint weaknesses identified by Defender.

### Additional integration options

**App protection policies**: You can use [app protection policies](../protect/microsoft-defender-integrate.md#create-and-assign-app-protection-policy-to-set-device-risk-level) to set device risk levels for both enrolled and unenrolled devices. This provides app-level protection based on Defender threat assessments.

**Unenrolled devices**: For devices that aren't or can't enroll in Intune, use Intune's [security management for Microsoft Defender for Endpoint](mde-security-integration.md) to manage Defender settings via endpoint security policies without requiring full device enrollment.

Before you begin any of these integration workflows, ensure you have the required licenses and platform configurations.

## Prerequisites

### Intune requirements

**Subscription**: Microsoft Intune Plan 1 subscription provides access to Intune and the Microsoft Intune admin center.

For licensing options, see [Microsoft Intune licensing](../fundamentals/licenses.md).

**Supported platforms**:

| Platform | Requirements |
|----------|--------------|
| Android  | Intune-managed devices |
| iOS/iPadOS | Intune-managed devices |
| Windows  | Microsoft Entra ID hybrid joined or Microsoft Entra ID joined |

### Microsoft Defender for Endpoint requirements

**Subscription**: Microsoft Defender for Endpoint subscription provides access to the [Microsoft Defender XDR portal](https://go.microsoft.com/fwlink/p/?linkid=2077139).

For licensing and system requirements, see:
- [Licensing requirements in Microsoft Defender for Endpoint minimum requirements](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements)
- [Microsoft 365 E5 trial subscription setup](/microsoft-365/security/defender/setup-m365deval#enable-microsoft-365-trial-subscription)
- [Microsoft Defender for Endpoint system requirements](/defender-endpoint/minimum-requirements#hardware-and-software-requirements)

## 📌 Real-world scenario: Stopping a phishing attack

This example shows how Microsoft Defender for Endpoint and Intune work together to automatically contain threats. In this scenario, the integration is already configured.

### How the attack unfolds

1. **Initial compromise**: A user receives a Word document via email containing embedded malicious code.
2. **User action**: The user opens the attachment and enables macros.
3. **Privilege escalation**: The malware gains elevated privileges on the device.
4. **Lateral movement**: The attacker attempts to access other corporate resources through the compromised device.

### How the integration prevents the breach

1. **Detection**: Microsoft Defender for Endpoint detects:
   - Abnormal code execution
   - Process privilege escalation
   - Malicious code injection
   - Suspicious remote shell activity

2. **Risk assessment**: Based on these threat indicators, Microsoft Defender for Endpoint [classifies the device as high-risk](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) and creates a detailed report in the Microsoft Defender XDR portal.

3. **Compliance enforcement**: Your Intune device compliance policy automatically marks devices with *Medium* or *High* risk levels as noncompliant.

4. **Access blocking**: Conditional Access policies immediately block the compromised device from accessing corporate resources.

5. **Containment**: The threat is contained while security teams investigate and remediate.

> [!NOTE]
> You can integrate Microsoft Defender for Endpoint with Microsoft Intune as a Mobile Threat Defense (MTD) solution, meaning Defender acts as the threat detection engine for Intune's compliance decisions.

### Platform-specific capabilities

Different platforms offer unique configuration options when integrating with Microsoft Defender for Endpoint:

**Android**: Use Intune device configuration policies to configure [Microsoft Defender for Endpoint web protection](../protect/microsoft-defender-configure-android.md) settings, including the ability to enable or disable VPN-based scanning.

**iOS/iPadOS**: Enable [vulnerability assessment of apps](/microsoft-365/security/defender-endpoint/ios-configure-features#configure-vulnerability-assessment-of-apps) to allow Defender to analyze app metadata from Intune for enhanced threat detection.

**Windows**: Benefit from automatic onboarding capabilities and use [Microsoft Defender for Endpoint security baselines](../protect/security-baselines.md) for comprehensive, prescriptive security configurations.

## Next steps

**Ready to set this up?** Continue to the configuration guide that follows for step-by-step instructions.

### Configure the integration

**Primary guide**: [Configure Microsoft Defender for Endpoint in Intune](../protect/microsoft-defender-integrate.md) - Complete step-by-step instructions for connecting, onboarding devices, and configuring Conditional Access policies.

### Expand your knowledge

**Intune resources**:

- [Use security tasks with Defender for Endpoint's Vulnerability Management to remediate device issues](atp-manage-vulnerabilities.md)
- [Get started with device compliance policies](device-compliance-get-started.md)

**Microsoft Defender for Endpoint resources**:

- [Microsoft Defender for Endpoint Conditional Access](/defender-endpoint/conditional-access)
- [Microsoft Defender XDR portal](/defender-xdr/microsoft-365-defender-portal)