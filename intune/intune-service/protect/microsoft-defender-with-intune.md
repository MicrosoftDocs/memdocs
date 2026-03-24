---
title: Integrate Microsoft Defender for Endpoint with Intune for Device Compliance
description: Integrate Microsoft Defender for Endpoint with Microsoft Intune as a Mobile Threat Defense (MTD) solution to enforce device compliance and prevent security breaches.
author: brenduns
ms.author: brenduns
ms.date: 03/24/2026
ms.topic: article
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- highpri
- sub-secure-endpoints
---

# Integrate Microsoft Defender for Endpoint with Intune for Device Compliance

Integrating Microsoft Defender for Endpoint with Microsoft Intune lets you assess device risk in real time and block compromised devices from corporate resources by automatically marking them as noncompliant.

For example, if malware compromises a user's device, Microsoft Defender for Endpoint flags that device as high-risk and Intune can automatically cut off its access to corporate resources.

## Integration workflow

The following workflow applies to devices enrolled with Intune. For detailed instructions, see [Configure Microsoft Defender for Endpoint in Intune](../protect/microsoft-defender-integrate.md):

1. [Establish a service-to-service connection](../protect/microsoft-defender-integrate.md#connect-microsoft-defender-for-endpoint-to-intune) between Intune and Microsoft Defender for Endpoint.
2. [Onboard devices](../protect/microsoft-defender-integrate.md#onboard-devices) with Microsoft Defender for Endpoint using Intune policy.
3. [Create a device compliance policy](../protect/microsoft-defender-integrate.md#create-and-assign-compliance-policy-to-set-device-risk-level) to set acceptable risk levels.
4. [Configure Conditional Access policy](../protect/microsoft-defender-integrate.md#create-a-conditional-access-policy) to block noncompliant devices.

**Extend the integration:** Once configured, you can [use Microsoft Defender Vulnerability Management](atp-manage-vulnerabilities.md) to remediate endpoint weaknesses identified by Defender.

## Additional integration options

**App protection policies**: You can use [app protection policies](../protect/microsoft-defender-integrate.md#create-and-assign-app-protection-policy-to-set-device-risk-level) to set device risk levels for both enrolled and unenrolled devices. This provides app-level protection based on Defender threat assessments.

**Unenrolled devices**: For devices that aren't or can't enroll in Intune, use Intune's [security management for Microsoft Defender for Endpoint](mde-security-integration.md) to manage Defender settings via endpoint security policies without requiring full device enrollment.

## Prerequisites

### Role-based access control

To configure the Defender for Endpoint integration, your account must be assigned an Intune role-based access control (RBAC) role that includes the following permissions:

- **Mobile Threat Defense**: *Modify* and *Read* – Required to establish the service-to-service connection between Intune and Defender.
- **Endpoint Detection and Response**: *Assign*, *Create*, *Read*, and *Update* – Required to onboard devices using Intune EDR policy.
- **Device compliance policies**: *Assign*, *Create*, *Read*, and *Update* – Required to configure risk-level compliance policies.

You can add these permissions to a [custom Intune role](../fundamentals/create-custom-role.md), or use the built-in **Endpoint Security Manager** role, which is the least-privileged built-in Intune role that includes all required permissions. For details, see [Role-based access control for Microsoft Intune](../fundamentals/role-based-access-control.md).

> [!NOTE]
> Conditional Access policies are configured in Microsoft Entra ID and require a separate Entra ID role, such as [Conditional Access Administrator](/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).

### Intune requirements

**Subscription**: Microsoft Intune Plan 1 subscription provides access to Intune and the Microsoft Intune admin center.

For licensing options, see [Microsoft Intune licensing](../../fundamentals/licensing/index.md).

**Supported platforms**:

| Platform | Requirements |
|----------|--------------|
| Android  | Intune-managed devices |
| iOS/iPadOS | Intune-managed devices |
| Windows  | Microsoft Entra ID hybrid joined or Microsoft Entra ID joined |

### Microsoft Defender for Endpoint requirements

**Subscription**: Microsoft Defender for Endpoint subscription provides access to the [Microsoft Defender XDR portal](https://go.microsoft.com/fwlink/p/?linkid=2077139).

For licensing and system requirements, see [Minimum requirements for Microsoft Defender for Endpoint](/defender-endpoint/minimum-requirements).

## Real-world scenario: Stopping a phishing attack

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

2. **Risk assessment**: Based on these threat indicators, Microsoft Defender for Endpoint classifies the device as high-risk and creates a detailed report in the Microsoft Defender XDR portal.

3. **Compliance enforcement**: Your Intune device compliance policy automatically marks devices with *Medium* or *High* risk levels as noncompliant.

4. **Access blocking**: Conditional Access policies immediately block the compromised device from accessing corporate resources.

5. **Containment**: The threat is contained while security teams investigate and remediate.

### Platform-specific capabilities

Different platforms offer unique configuration options when integrating with Microsoft Defender for Endpoint:

**Android**: Use Intune device configuration policies to configure [Microsoft Defender for Endpoint web protection](../protect/microsoft-defender-configure-android.md) settings, including the ability to enable or disable VPN-based scanning.

**iOS/iPadOS**: Enable [vulnerability assessment of apps](/defender-endpoint/ios-configure-features#configure-vulnerability-assessment-of-apps) to allow Defender to scan installed apps for known vulnerabilities.

**Windows**: Benefit from automatic onboarding capabilities and use [Microsoft Defender for Endpoint security baselines](../protect/security-baselines.md) for comprehensive, prescriptive security configurations.

## Next steps

### Configure the integration

[Configure Microsoft Defender for Endpoint in Intune](../protect/microsoft-defender-integrate.md): complete step-by-step instructions for connecting Intune and Defender, onboarding devices, and setting up Conditional Access policies.

### Related content

**Intune resources**:

- [Use security tasks with Defender for Endpoint's Vulnerability Management to remediate device issues](atp-manage-vulnerabilities.md)
- [Get started with device compliance policies](device-compliance-get-started.md)

**Microsoft Defender for Endpoint resources**:

- [Microsoft Defender for Endpoint Conditional Access](/defender-endpoint/conditional-access)
- [Microsoft Defender XDR portal](/defender-xdr/microsoft-365-defender-portal)