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

For an overview of how Intune supports Zero Trust principles (verify explicitly, use least privilege access, and assume breach), see [Zero Trust with Microsoft Intune](zero-trust-with-microsoft-intune.md).

## Seven-layer Zero Trust deployment progression

Building a comprehensive Zero Trust security posture for devices involves progressively implementing layers of protection. Each layer builds on the previous one, starting with basic data protection and advancing to sophisticated threat detection and data loss prevention.

The following table shows recommended deployment progression for Zero Trust device security:

| Layer | Protection capability | What you accomplish | Prerequisites | License requirements |
|-------|----------------------|---------------------|---------------|---------------------|
| **1** | [App protection policies](deployment-plan-protect-apps.md) | Protect organizational data in apps without requiring device enrollment. Creates foundation for bring-your-own-device (BYOD) scenarios. | Supported apps (Microsoft 365 apps, policy-enabled apps) | Microsoft 365 E3, E5, F1, F3, F5 |
| **2** | [Enroll devices](deployment-guide-enrollment.md) | Establish relationship between user, device, and Intune. Enable device management and visibility into endpoints accessing resources. | Platform-specific prerequisites (MDM authority, certificates) | Microsoft 365 E3, E5, F1, F3, F5 |
| **3** | [Compliance policies](deployment-plan-compliance-policies.md) | Define minimum requirements devices must meet (password protection, OS version, encryption). Mark devices as compliant or noncompliant. | Devices enrolled in layer 2 | Microsoft 365 E3, E5, F3, F5 |
| **4** | [Require healthy and compliant devices](../protect/device-compliance-get-started.md#integrate-with-conditional-access) | Implement enterprise Zero Trust identity and device access policies. Work with identity team to enforce compliance through Conditional Access, blocking access from devices that don't meet security requirements. | Compliance policies from layer 3, coordination with identity administrators | Microsoft 365 E3, E5, F3, F5 |
| **5** | [Configuration profiles](deployment-plan-configuration-profile.md) | Configure device settings to harden security. Deploy security baselines. Move security controls from Group Policy to cloud policies. | Enrolled devices from layer 2 | Microsoft 365 E3, E5, F3, F5 |
| **6** | [Device risk monitoring](../protect/microsoft-defender-integrate.md) | Integrate with Microsoft Defender for Endpoint to monitor device risk, detect threats, and block access based on risk level. Deploy security baselines. | Microsoft Defender for Endpoint setup, coordination with threat protection team | Microsoft 365 E5, F5 |
| **7** | [Endpoint DLP](/purview/endpoint-dlp-learn-about) | Protect sensitive data on endpoints with Microsoft Purview Data Loss Prevention. Monitor and control file operations based on sensitivity labels. | Microsoft Purview configuration, devices onboarded to MDE in layer 6 | Microsoft 365 E5, E5 compliance add-on, F5 compliance add-on |

## Understanding the seven deployment layers

This section explains each layer in the Zero Trust deployment progression. While the [seven-layer table](#seven-layer-zero-trust-deployment-progression) shows what each layer accomplishes, these descriptions provide context, examples, and clarification of key concepts.

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

### Compliance policies (Layer 3)

Compliance policies define security requirements that devices must meet to access organizational resources. These policies evaluate device health and mark devices as compliant or noncompliant based on settings you configure, such as password requirements, OS versions, encryption status, and jailbreak detection.

**Example:** Your compliance policy requires Windows devices to have BitLocker enabled, run a minimum OS version, and use a password with at least eight characters. A user's laptop missing BitLocker is marked noncompliant. The user receives notifications about the requirement and has time to remediate before access is blocked (if you enforce layer 4).

> [!TIP]
> Compliance policies assess device state but don't automatically block access. They work with Conditional Access (layer 4) to enforce compliance requirements.

For details, see [Deployment guidance: Compliance policies](deployment-plan-compliance-policies.md).

### Require healthy and compliant devices (Layer 4)

This layer implements enterprise-level Zero Trust identity and device access policies by requiring devices to be healthy and compliant before granting access to organizational resources. You work with your identity team to create Conditional Access policies in Microsoft Entra ID that enforce the compliance decisions from layer 3.

This layer represents the shift from assessment to enforcement. After compliance policies mark devices as compliant or noncompliant, Conditional Access policies use that signal to grant or block access to email, SharePoint, Teams, and other protected resources.

**Example:** Your identity team creates a Conditional Access policy requiring compliant devices for all users accessing Microsoft 365 apps. A user with a noncompliant device (missing BitLocker from the layer 3 example) attempts to access Outlook. The Conditional Access policy blocks access and displays a message explaining the device doesn't meet security requirements. After a device enables BitLocker and checks in with Intune, the device is assessed as compliant and access is restored.

> [!NOTE]
> This layer requires coordination with your identity team, as Conditional Access policies are created in Microsoft Entra ID, not Intune. See the [Identity team coordination section](#identity-team-microsoft-entra-id) for the workflow.

For details, see [Require managed devices with Conditional Access](/entra/identity/conditional-access/policy-all-users-device-compliance).

### Configuration profiles (Layer 5)

Configuration profiles configure device settings to harden security, enable features, and create consistent configurations across your fleet. While compliance policies (layer 3) assess whether devices meet requirements, configuration profiles proactively deploy settings to ensure devices are configured correctly.

Common configurations include security baselines, Wi-Fi and VPN profiles, certificate deployment, password policies, disk encryption settings, and application of Group Policy equivalents.

**Example:** You deploy a Windows security baseline to corporate laptops. The configuration profile enables Windows Firewall, configures BitLocker encryption, disables legacy protocols, enables attack surface reduction rules, and configures dozens of other security settings. Users don't need to configure any of these settings manually—Intune applies them automatically.

> [!TIP]
> Security baselines are preconfigured profiles containing Microsoft's recommended security settings. Use them as a starting point, then customize based on your organization's needs.

For details, see [Deploy configuration profiles](deployment-plan-configuration-profile.md).

### Device risk monitoring (Layer 6)

Device risk monitoring integrates Microsoft Defender for Endpoint with Intune to add continuous threat detection, device risk assessment, and risk-based access controls. This layer shifts from static compliance checks to dynamic security monitoring that responds to active threats in real time.

When you onboard devices to Microsoft Defender for Endpoint, they begin reporting security telemetry and threat intelligence. Defender assigns each device a risk level (secure, low, medium, high, or unavailable) based on detected threats, vulnerabilities, and security posture. You can use this risk level in compliance policies to block access from high-risk devices or trigger remediation actions.

**Example:** A user's laptop becomes infected with malware. Microsoft Defender for Endpoint detects the threat and marks the device as high risk. Your compliance policy evaluating device risk immediately marks the device as noncompliant. Conditional Access blocks the user's access to organizational resources until Defender remediates the threat and the device risk returns to an acceptable level.

> [!TIP]
> This layer also enables deployment of the Microsoft Defender for Endpoint security baseline, which configures advanced threat protection settings like attack surface reduction rules, controlled folder access, and network protection.

For details, see [Microsoft Defender for Endpoint integration](../protect/microsoft-defender-integrate.md).

### Endpoint data loss prevention (Layer 7)

Endpoint data loss prevention uses Microsoft Purview to prevent sensitive data from leaving managed endpoints through copy, print, upload, or transfer operations. While earlier layers protect access to resources, this layer protects the data itself by monitoring and controlling how users interact with sensitive files.

Devices onboarded to Microsoft Defender for Endpoint in layer 6 are automatically onboarded for Endpoint DLP with no additional Intune configuration. Your compliance team creates DLP policies in the Microsoft Purview portal defining which sensitivity labels, file types, or content patterns trigger protective actions.

**Example:** Your compliance team creates a DLP policy preventing files labeled "Confidential" from being copied to USB drives or uploaded to personal cloud storage. A user attempts to copy a confidential financial report to a USB drive. Endpoint DLP blocks the operation and displays a policy notification explaining the restriction. The user can file a business justification to request an override if needed, and all activities are logged for compliance reporting.

> [!NOTE]
> As the Intune administrator, your role for Endpoint DLP is limited to ensuring devices are onboarded to Microsoft Defender for Endpoint (layer 6). All DLP policy creation and management happens in the Microsoft Purview portal by your compliance team.

For details, see [Learn about Endpoint DLP](/purview/endpoint-dlp-learn-about) and [Get started with Endpoint DLP](/purview/endpoint-dlp-getting-started).

## Enrollment vs. onboarding

As you implement these layers, you'll work with two related but different concepts: **enrollment** and **onboarding**. Understanding the difference helps clarify what happens at each layer.

**Enrollment** (Layer 2) registers devices with Intune for comprehensive device management. **Onboarding** (Layers 6-7) configures devices to report information to specific services like Microsoft Defender for Endpoint or Microsoft Purview.

|  | Enrollment | Onboarding |
|---------|---------|----------|
| **What it does** | Registers devices for management with Intune. Intune manages the entire device including apps, settings, and policies. | Configures devices to share information with specific Microsoft 365 services (currently Microsoft Defender for Endpoint and Microsoft Purview). |
| **Scope** | Full device management—configure settings, deploy apps, enforce compliance, monitor device health. | Service-specific capabilities only. For example, onboarding to MDE enables threat detection; onboarding to Purview enables DLP. |
| **In this deployment** | Layer 2: You enroll devices into Intune management. | Layer 6: You onboard devices to Microsoft Defender for Endpoint using Intune.<br>Layer 7: Devices onboarded to MDE are automatically onboarded for Microsoft Purview Endpoint DLP. |
| **How you do it** | Platform-specific enrollment methods: Microsoft Entra join (automatic enrollment), Windows Autopilot, Apple Automated Device Enrollment, manual enrollment. | Use Intune to deploy onboarding configuration to enrolled devices. Devices must be enrolled in Intune before you can onboard them to MDE or Purview. |

> [!NOTE]
> Onboarding to Microsoft Defender for Endpoint automatically onboards devices for Microsoft Purview capabilities including Endpoint DLP. No additional Intune configuration is required.

## Coordinating with Microsoft 365 teams

Implementing Zero Trust device security requires coordination across multiple teams in your organization. While you manage Intune policies, other teams manage complementary services that work together to enforce protection.

### Identity team (Microsoft Entra ID)

**Your coordination:**

- After you create app protection policies (layer 1), work with identity team to create Conditional Access policy requiring approved apps.
- After creating compliance policies (layer 3), coordinate Conditional Access policy requiring compliant devices:
  1. You create and assign compliance policies in Intune to define device requirements.
  2. Identity team creates Conditional Access policy in Microsoft Entra admin center.
  3. Conditional Access policy uses "Require device to be marked as compliant" grant control.
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

## Next steps

**Get started with Zero Trust device security:**

- [Deployment guidance: App protection policies](deployment-plan-protect-apps.md) - Layer 1
- [Deployment guidance: Enroll devices](deployment-guide-enrollment.md) - Layer 2
- [Deployment guidance: Compliance policies](deployment-plan-compliance-policies.md) - Layer 3
- [Require managed devices with Conditional Access](/entra/identity/conditional-access/policy-all-users-device-compliance) - Layer 4

**Learn more about Zero Trust:**

- [Zero Trust Guidance Center](/security/zero-trust) - Enterprise-scale strategy and architecture
- [Secure endpoints with Zero Trust](/security/zero-trust/deploy/endpoints) - Device-centric deployment objectives
- [Zero Trust deployment plan with Microsoft 365](/microsoft-365/security/microsoft-365-zero-trust) - Cross-service deployment guidance

**Explore advanced protection layers:**

- [Deploy configuration profiles](deployment-plan-configuration-profile.md) - Layer 5
- [Microsoft Defender for Endpoint integration](../protect/microsoft-defender-integrate.md) - Layer 6
- [Learn about Endpoint DLP](/purview/endpoint-dlp-learn-about) - Layer 7
