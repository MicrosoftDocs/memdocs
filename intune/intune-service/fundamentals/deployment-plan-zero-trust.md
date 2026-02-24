---
title: Zero Trust deployment approach with Microsoft Intune
description: Learn the recommended seven-layer deployment progression for implementing Zero Trust device security with Microsoft Intune, from app protection to endpoint data loss prevention.
author: brenduns
ms.author: brenduns
ms.date: 02/24/2026
ms.topic: concept-article
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.collection:
- M365-identity-device-management
- highpri
- zerotrust-services
---

# Zero Trust deployment approach with Microsoft Intune

Microsoft Intune is a mobile device management solution that supports your organization's Zero Trust journey.

[Zero Trust](/security/zero-trust/zero-trust-overview) isn't a product or service. Instead, it's a modern cybersecurity strategy that assumes no implicit trust, not even within the corporate network. Instead of trusting users, devices, or applications by default, a Zero Trust approach explicitly verifies every access request, continuously assesses risk, and enforces least privilege access across the entire digital estate.

Core principles of Zero Trust include:

| Verify explicitly | Use least privilege access | Assume breach |
|---------|---------|---------|
| Always authenticate and authorize based on all available data points. | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

## Why manage endpoints for Zero Trust?

The modern enterprise has incredible diversity in endpoints accessing organizational data. Users work from anywhere, from any device, more than at any time in history. This creates a massive attack surface, and endpoints can easily become the weakest link in your Zero Trust security strategy.

While organizations are typically proactive in protecting PCs from vulnerabilities and attacks, mobile devices often go unmonitored and without protections. Gaining visibility into endpoints that access your corporate resources is the first step in your Zero Trust device strategy.

To avoid exposing your data to risk, you need to monitor every endpoint for risks and employ granular access controls to deliver the appropriate level of access based on organizational policy. For example, if a personal device is jailbroken, you can block its access to prevent enterprise applications from being exposed to known vulnerabilities.

## Device and application authentication, authorization, and protection for Zero Trust

You can use Intune to protect both access and data on organization-owned devices and your user's personal devices that they use for work. Intune use of Microsoft Entra as its identity service helps you enforce device compliance policies that align with your organization's requirements while providing reports that help you monitor and achieve your Zero Trust objectives.

| Zero Trust principle | How Intune helps |
|----------------------|------------------|
| Verify explicitly | Intune supports creation of policies for [apps](../apps/app-protection-policy.md), [security settings](../protect/security-baselines-configure.md), [device configuration](../configuration/settings-catalog.md), [compliance](../protect/device-compliance-get-started.md), Microsoft Entra [Conditional Access](../protect/conditional-access.md), and more. These policies become part of the authentication and authorization process of accessing resources. |
| Use least privilege access | Intune simplifies app management with a built-in app experience, including app lifecycle management. You can distribute apps from your private app stores, enable Microsoft 365 apps, deploy Win32 apps, create app protection policies, and manage access to apps and their data.</br></br> Intune's [Endpoint Privilege Management (EPM)](../protect/epm-overview.md) helps you move your organization's users to run as standard users without administrator rights while enabling those same users to complete tasks and run apps that require elevated privileges.</br></br> Intune policies for Local Administrator Password Solutions (LAPS) for both [Windows](../protect/windows-laps-overview.md) and [macOS](../enrollment/macos-laps.md) can help you secure and manage the local administrator accounts on your managed devices. |
| Assume breach | Intune integrates with [mobile threat defense services](../protect/mobile-threat-defense.md), including Microsoft Defender for Endpoint and third-party partner services. With these services, you can create policies for endpoint protection that respond to threats, do real-time risk analysis, and automate remediation.</br></br> When you integrate Intune and Defender, you can use evolving tools like the [Vulnerability Remediation Agent for Security Copilot](../../agents/vulnerability-remediation-agent.md). This agent identifies Common Vulnerabilities and Exposures (CVEs) on your managed devices and provides you with step-by-step guidance you can use to remediate them. |

## Seven-layer Zero Trust deployment progression

Building a comprehensive Zero Trust security posture for devices involves progressively implementing layers of protection. Each layer builds on the previous one, starting with basic data protection and advancing to sophisticated threat detection and data loss prevention.

The following table shows recommended deployment progression for Zero Trust device security:

| Layer | Protection capability | What you accomplish | Prerequisites | License requirements |
|-------|----------------------|---------------------|---------------|---------------------|
| **1** | [App protection policies](deployment-plan-protect-apps.md) | Protect organizational data in apps without requiring device enrollment. Creates foundation for bring-your-own-device (BYOD) scenarios. | Supported apps (Microsoft 365 apps, policy-enabled apps) | Microsoft 365 E3, E5, F1, F3, F5 |
| **2** | [Enroll devices](deployment-guide-enrollment.md) | Establish relationship between user, device, and Intune. Enable device management and visibility into endpoints accessing resources. | Platform-specific prerequisites (MDM authority, certificates) | Microsoft 365 E3, E5, F1, F3, F5 |
| **3** | [Compliance policies](deployment-plan-compliance-policies.md) | Define minimum requirements devices must meet (password protection, OS version, encryption). Mark devices as compliant or noncompliant. | Devices enrolled in layer 2 | Microsoft 365 E3, E5, F3, F5 |
| **4** | [Require compliant devices](../protect/device-compliance-get-started.md#integrate-with-conditional-access) | Work with identity team to enforce compliance through Microsoft Entra Conditional Access policies. Block access from noncompliant devices. | Compliance policies from layer 3, coordination with identity administrators | Microsoft 365 E3, E5, F3, F5 |
| **5** | [Configuration profiles](deployment-plan-configuration-profile.md) | Configure device settings to harden security. Deploy security baselines. Move security controls from Group Policy to cloud policies. | Enrolled devices from layer 2 | Microsoft 365 E3, E5, F3, F5 |
| **6** | [Device risk monitoring](../protect/microsoft-defender-integrate.md) | Integrate with Microsoft Defender for Endpoint to monitor device risk, detect threats, and block access based on risk level. Deploy security baselines. | Microsoft Defender for Endpoint setup, coordination with threat protection team | Microsoft 365 E5, F5 |
| **7** | [Endpoint DLP](/purview/endpoint-dlp-learn-about) | Protect sensitive data on endpoints with Microsoft Purview Data Loss Prevention. Monitor and control file operations based on sensitivity labels. | Microsoft Purview configuration, devices onboarded to MDE in layer 6 | Microsoft 365 E5, E5 compliance add-on, F5 compliance add-on |

### Progressive levels of protection

As you advance through these layers, the sophistication of protection increases:

- **Unmanaged devices** - App protection policies control access to organizational data in apps
- **Enrolled devices with compliance** - Enrollment and compliance policies provide device visibility and security posture assessment
- **Compliance enforcement** - Conditional Access policies block access from noncompliant devices
- **Hardened devices** - Configuration profiles apply security baselines and settings across enrolled devices
- **Threat-aware access** - Microsoft Defender for Endpoint integration adds device risk monitoring and risk-based access controls
- **Data loss prevention** - Microsoft Purview Endpoint DLP prevents sensitive data from leaving managed endpoints

This approach allows you to start protecting data immediately (layer 1) while planning for more comprehensive device management (layers 2-7).

## Coordinating with Microsoft 365 teams

Implementing Zero Trust device security requires coordination across multiple teams in your organization. While you manage Intune policies, other teams manage complementary services that work together to enforce protection.

### Identity team (Microsoft Entra ID)

**Your coordination:**

- After creating app protection policies (layer 1), work with identity team to create Conditional Access policy requiring approved apps.
- After creating compliance policies (layer 3), coordinate Conditional Access policy requiring compliant devices:
  1. You create and assign compliance policies in Intune to define device requirements.
  2. Identity team creates Conditional Access policy in Microsoft Entra admin center.
  3. CA policy uses "Require device to be marked as compliant" grant control.
  4. Ensure both policies target the same user groups.
  5. Test together using the Conditional Access *What If* tool before enabling enforcement.
- For detailed workflow, see [Common ways to use Conditional Access](../protect/conditional-access-intune-common-ways-use.md#device-based-conditional-access).
- For policy creation, see [Require managed devices with Conditional Access](/entra/identity/conditional-access/policy-all-users-device-compliance).

**Related guidance:** [Conditional Access with Intune](../protect/conditional-access.md)

### Threat protection team (Microsoft Defender)

**Their responsibility:** Set up and manage Microsoft Defender for Endpoint service, investigate threats, and manage security operations center (SOC) workflows.

**Your coordination:**

- Use Intune to onboard devices to Microsoft Defender for Endpoint (layer 6)
- Deploy both Windows security baseline and Defender for Endpoint security baseline to managed devices
- Receive device risk signals from Defender that feed into compliance policies
- Coordinate incident response when threats are detected on managed devices

**Related guidance:** [Microsoft Defender for Endpoint integration](../protect/microsoft-defender-integrate.md)

### Data security and privacy team (Microsoft Purview)

**Their responsibility:** Define data sensitivity schema, create DLP policies, and manage compliance requirements in Microsoft Purview.

**Your coordination:**

- Ensure devices are onboarded to support Endpoint DLP (automatic with MDE onboarding in layer 6)
- Identify which user groups should be included/excluded from DLP policies
- Verify device visibility in [Microsoft Purview portal](https://compliance.microsoft.com)
- Support user education when DLP policies block or warn about data operations

> [!NOTE]
> As the Intune administrator, your role for Endpoint DLP is limited to ensuring devices are onboarded to Microsoft Defender for Endpoint. Devices onboarded to MDE automatically become DLP-capable with no additional Intune configuration. All DLP policy creation and management happens in the Microsoft Purview portal by your compliance team.

**Related guidance:** [Learn about Endpoint DLP](/purview/endpoint-dlp-learn-about) | [Get started with Endpoint DLP](/purview/endpoint-dlp-getting-started)

### Best practices for cross-team coordination

- **Establish regular coordination meetings** during initial deployment of each layer.
- **Document ownership** - Be clear about which team manages which policies.
- **Test together** - Use audit mode and What If tools before enforcement.
- **Align on user groups** - Ensure consistent group assignments across services.
- **Plan communications** - Coordinate user notifications when policies might impact user experience.
- **Share monitoring responsibilities** - Each team monitors their service, but share insights about user impact.

## Understanding app protection, enrollment, and onboarding

As you implement the Zero Trust deployment progression, you work with three different approaches to protecting data and devices:

- **App protection without enrollment (MAM-WE)** - Apply policies to apps on unmanaged devices (layer 1).
- **Enrollment** - Register devices with Intune for full device management (layer 2).
- **Onboarding** - Configure devices to report to Microsoft Defender for Endpoint and Microsoft Purview (layers 6-7).

### App protection without enrollment (Layer 1)

App protection policies protect organizational data within apps, controlling how users access and share work data. Layer 1 focuses on protecting data on **unmanaged personal devices** without requiring enrollment, but app protection policies can also be applied to enrolled devices for defense-in-depth.

Users install apps like Outlook or Teams from the store, sign in with their work account, and data protection policies automatically apply. This approach is commonly called **MAM without enrollment** or **bring-your-own-device (BYOD)**.

**Example:** A user's personal iPhone has Outlook installed. Your app protection policy requires a PIN to access work email, prevents copying work data to personal apps, and blocks saving email attachments to personal cloud storage. The user maintains full control of their device while organizational data stays protected.

> [!TIP]
> App protection policies can be deployed to both unenrolled devices (layer 1) and enrolled devices (layer 2+) for additional app-level protection beyond device management.

For details, see [Deployment guidance: App protection policies](deployment-plan-protect-apps.md).

### Device enrollment (Layer 2)

Enrollment registers devices with Intune, enabling comprehensive device management. Intune deploys apps, configures settings, enforces compliance policies, and provides complete visibility into the device state.

**Example:** A corporate laptop enrolls in Intune during Windows Autopilot setup. Intune configures Wi-Fi, deploys certificates, installs security baselines, enforces BitLocker encryption, and monitors compliance with your password policy.

For details, see [Deployment guidance: Enroll devices](deployment-guide-enrollment.md).

### Device onboarding (Layers 6-7)

Onboarding enables devices to share security and compliance telemetry with Microsoft Defender for Endpoint and Microsoft Purview. This happens independently of enrollment:

1. **Onboard devices** to Microsoft Defender for Endpoint (layer 6) for threat detection and device risk assessment.
2. Devices onboarded to Defender are **automatically onboarded** for Microsoft Purview Endpoint DLP (layer 7) with no additional configuration.

**Example:** After enrolling corporate laptops in layer 2, you use Intune to deploy the Microsoft Defender for Endpoint configuration. Devices begin reporting threat intelligence to Defender and automatically gain Endpoint DLP capabilities. Your compliance team can now create DLP policies in Purview to prevent sensitive data from being copied to USB drives.

> [!NOTE]
> Devices can be onboarded without being enrolled (for example, using Group Policy on domain-joined machines), but the recommended approach for consistency is to use Intune for both enrollment and onboarding.

For details, see [Microsoft Defender for Endpoint integration](../protect/microsoft-defender-integrate.md) and [Learn about Endpoint DLP](/purview/endpoint-dlp-learn-about).

## Next steps

**Get started with Zero Trust device security:**

- [Deployment guidance: App protection policies](deployment-plan-protect-apps.md) - Layer 1
- [Deployment guidance: Enroll devices](deployment-guide-enrollment.md) - Layer 2
- [Deployment guidance: Compliance policies](deployment-plan-compliance-policies.md) - Layer 3

**Learn more about Zero Trust:**

- [Zero Trust Guidance Center](/security/zero-trust) - Enterprise-scale strategy and architecture
- [Secure endpoints with Zero Trust](/security/zero-trust/deploy/endpoints) - Device-centric deployment objectives
- [Zero Trust deployment plan with Microsoft 365](/microsoft-365/security/microsoft-365-zero-trust) - Cross-service deployment guidance

**Explore advanced protection layers:**

- [Deploy configuration profiles](deployment-plan-configuration-profile.md) - Layer 5
- [Microsoft Defender for Endpoint integration](../protect/microsoft-defender-integrate.md) - Layer 6
- [Learn about Endpoint DLP](/purview/endpoint-dlp-learn-about) - Layer 7
