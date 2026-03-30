---
title: Secure Your Corporate Data in Intune with Microsoft Edge for Business
description: Secure your corporate data in Microsoft Intune with Microsoft Edge for Business across all platforms.
ms.date: 01/15/2026
ms.topic: overview
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Secure Your Corporate Data in Intune with Microsoft Edge for Business

This comprehensive guide helps you implement a complete Secure Enterprise Browser strategy using Microsoft Edge for Business and Microsoft Intune across all platforms.

**Applies to:**

- Microsoft Edge for Business
- Microsoft Intune Mobile Application Management (MAM)
- Microsoft Intune Mobile Device Management (MDM)
- Platforms: Windows, macOS, iOS, and Android

## Target Audience

The target audience for this content includes:

- **Intune Administrators:** This content provides detailed guidance about configuring and managing Microsoft Edge for Business across all platforms in Microsoft Intune.
- **Security Professionals:** This document provides security professionals with a structured approach to browser security, outlining key controls, risk mitigation strategies, and alignment with industry security frameworks.
- **IT Architects:** This content helps architects design secure browser solutions that balance security requirements with user productivity across managed and unmanaged devices.
- **Decision Makers:** This content helps decision makers understand the security, productivity, and manageability benefits of implementing a comprehensive secure enterprise browser strategy.

> [!NOTE]
> This content is designed to help you use the full potential of Microsoft Edge for Business and Microsoft Application Management across all device platforms and management scenarios.

> [!IMPORTANT]
> The Secure Enterprise Browser framework references industry guidance such as NIST, DISA STIG, and CISA best practices. Applying the recommendations in this series alone doesn't guarantee compliance. Work with your compliance and security teams to validate requirements for your organization.

## Overview

This guide provides comprehensive step-by-step instructions to implement the Secure Enterprise Browser experience using the data protection framework:

1. **[Microsoft Entra Conditional Access with Microsoft Edge for Business](mamedge-1-mamca.md)** - Create Microsoft Entra Conditional Access policies and Intune app protection policies for browsing on Android, iOS, and Windows.
2. **[App protection policies for Microsoft Edge for Business](mamedge-2-app.md)** - Implement Level 1, Level 2, and Level 3 app protection policies for Windows, Android, and iOS platforms to ensure secure access and usage of enterprise applications.
3. **[Integrate Mobile Threat Defense](mamedge-3-scc.md)** - Enhance the overall security posture of your organization by integrating the secure enterprise browser with Windows Security Center, Microsoft Defender, or MTD partners.
4. **[App configuration policies for Microsoft Edge for Business](mamedge-4-acp-edge.md)** - Configure Level 1, Level 2, and Level 3 app configuration policies for Android, iOS, and Windows to customize browser behavior and features.
5. **[Settings catalog for Microsoft Edge for Business](mamedge-5-settings-catalog.md)** - Apply Level 1, Level 2, and Level 3 settings catalog configurations for Windows and macOS to establish comprehensive device-level browser controls.
6. **[Microsoft Edge for Business end user experience](mamedge-6-end-user-experience.md)** - Understand how security measures affecting user interaction for Microsoft Edge for Business.
7. **[Troubleshooting and FAQ](mamedge-7-troubleshoot.md)** - Troubleshoot app protection policies with validation examples and frequently asked questions.

> [!IMPORTANT]
> **Policy Selection Guidance**: When configuring browser policies for enrolled Windows devices, you should choose **either** Settings Catalog policies (Step 5) **or** the Microsoft Edge Security Baseline from Endpoint Security, not both. Implementing both creates policy conflicts. The Settings Catalog approach provides more flexibility and granular control across all three security levels. For comprehensive coverage, this guide focuses on Settings Catalog implementation.
>
> Similarly, for non-enrolled devices, use App Configuration Policies (Step 4). For enrolled devices, use Settings Catalog policies (Step 5). Never deploy both App Configuration Policies and Settings Catalog policies targeting Microsoft Edge to the same client as this creates policy conflicts.

For more information about Microsoft Edge Security content, see [Microsoft Edge for Business: AI and protection in one secure enterprise browser](https://aka.ms/EdgeSecuritywhitepaper).

### Security levels at a glance

| Level | Purpose | Typical users | Design goal | Productivity impact | Standards alignment |
| --- | --- | --- | --- | --- | --- |
| **Level 1 – Basic** | Establishes foundational hygiene and a secure data boundary. | General staff (≈80%). | Low-friction rollout that enables broad adoption. | Minimal disruption. | NIST basic controls, DISA STIG CAT III. |
| **Level 2 – Enhanced** | Strengthens data loss prevention (DLP) and tightens risky surfaces. | Managers, IT, HR, Finance (≈15%). | Reduce data exfiltration and enforce safer browsing. | Moderate—adds targeted prompts and blocks. | NIST moderate controls, DISA STIG CAT II. |
| **Level 3 – High** | Applies maximum isolation and least-privilege browsing. | Executives, SecOps, Legal, sensitive roles (≈5%). | Contain high-risk activity with provable assurances. | High by design to protect sensitive data. | NIST high controls, DISA STIG CAT I, CISA critical controls. |

These security levels describe **desired outcomes**. The linked implementation guides map those outcomes to policy tooling such as app protection policies, app configuration policies, settings catalog profiles, and conditional access.

### Required Microsoft Entra ID groups

Create security groups before building policies so you can target each level consistently:

- **Device groups:** `SEB-Level1-Devices`, `SEB-Level2-Devices`, `SEB-Level3-Devices`, `SEB-Excluded-Devices`.
- **User groups:** `SEB-Level1-Users`, `SEB-Level2-Users`, `SEB-Level3-Users`, `SEB-Excluded-Users`.

The level-specific groups support progressive assignments, while the exclusion groups provide safe testing and emergency access paths.

### Policy coverage across platforms

Use the following matrix to confirm which policy types apply at each level and platform before you dive into the step-by-step articles:

| Platform and policy type | Level 1 | Level 2 | Level 3 | Highlights |
| --- | --- | --- | --- | --- |
| Windows – Settings catalog | Core hygiene configuration. | Adds SmartScreen, application bound encryption, and broader extension controls. | Introduces Application Guard, URL allowlists, and strict update governance. | Primary device hardening for managed Windows endpoints. |
| Windows – App protection policies | Basic data protection with minimal sharing limits. | Blocks copy/paste and enforces device health checks. | Enables high assurance with secured threat levels and printer blocking. | Protects work data on managed and unmanaged Windows devices. |
| Windows – App configuration policies | Establishes home pages, password controls, and download policies. | Extends to certificate management, WebRTC, and session cleanup. | Forces allowlists, disables developer tools, and blocks downloads. | Deep browser customization without replacing device policies. |
| macOS – Settings catalog | Implements baseline protections and update management. | Adds developer tool lock down, WebUSB/WebHID blocks, and SmartScreen DNS. | Forces allowlist-only browsing with download and clipboard restrictions. | The settings catalog is the primary control plane for macOS. |
| iOS/iPadOS – App protection & configuration | Requires app PIN, encryption, and smart defaults. | Tightens backups, blocks screenshots, and limits sharing destinations. | Enforces biometric strength, URL allowlists, and high DLP settings. | Covers personal and corporate devices with MAM + ACP. |
| Android – App protection & configuration | Provides fundamental encryption, PIN, and SmartScreen settings. | Adds backup blocking, Play Integrity checks, and social-media blocks. | Requires Class 3 biometrics, kiosk options, and allowlist-only access. | Mirrors iOS protections with Android-specific controls. |
| Conditional Access (cross-platform) | Introduces browser-only access with MFA and APP requirements. | Adds device compliance, risk-based access, and session frequency controls. | Enforces high-trust locations, continuous access evaluation, and approved clients. | Complements policy configuration with identity-driven enforcement. |

## Secure Enterprise Browser

The Secure Enterprise Browser solution combines Microsoft Edge for Business with Microsoft Intune's comprehensive policy framework to create a secure, manageable browsing experience across all platforms. This solution extends the proven data protection framework beyond app protection policies to include app configuration policies and settings catalog configurations, providing a unified approach to securing enterprise browser deployments.

### Data Protection Framework for Secure Enterprise Browser

The data protection framework for the Secure Enterprise Browser builds on the established app protection policy framework and extends it to encompass all configuration aspects of Microsoft Edge for Business. This framework organizes security configurations into three levels:

- **Level 1 - Enterprise basic data protection**: The minimum recommended configuration for enterprise devices. This level provides fundamental security controls while maintaining user productivity.
- **Level 2 - Enterprise enhanced data protection**: Recommended for devices accessing sensitive or confidential information. This configuration applies to most users accessing work or school data and includes extra controls that might affect user experience.
- **Level 3 - Enterprise high data protection**: Designed for organizations with sophisticated security requirements or users at elevated risk. This configuration provides the highest level of protection for sensitive data.

Each level applies consistently across app protection policies, app configuration policies, and settings catalog configurations, allowing you to implement a cohesive security strategy tailored to your organization's needs.

### What is Microsoft Edge for Business?

Microsoft Edge for Business is your secure, productivity-first browser built for modern work. Designed for managed and unmanaged devices, it delivers enterprise-grade security and controls while maintaining the familiar Microsoft Edge experience you trust.

With automatic separation of work and personal browsing, Microsoft Edge for Business creates dedicated windows for each—complete with their own favorites, caches, and storage. This separation means no mix-ups, no accidental data leaks, and a seamless way to stay productive without compromising privacy.

Why choose Microsoft Edge for Business?

- **Secure by default** – Protect sensitive data effortlessly.
- **Built for productivity** – Enterprise features you already know, optimized for work.
- **Smart separation** – Keep work and personal browsing clearly apart.

### Is this a new browser?

No, this isn’t a new browser. This is a new, dedicated Microsoft Edge experience built specifically for work. It allows organizations to configure it to maximize productivity and security. It retains the same functionality that users are already familiar with in Microsoft Edge. Additionally, it offers an optional feature of automatic switching between personal and corporate accounts, designed to meet the evolving needs of users and businesses. Signing in with a Microsoft Entra ID will automatically enable the Microsoft Edge for Business experience.

### Benefits

Microsoft Edge for Business offers a multitude of advantages:

**Streamlined IT operations:** Microsoft Edge for Business can significantly reduce the cyber-attack surface area and enhance your organization’s security posture. It achieves this by streamlining down operations to a single browser for all use cases, simplifying IT management.

**Improved user experience:** For end users signed in with both work and personal profiles, Microsoft Edge for Business offers a superior browsing experience. The automatic switching feature not only enhances usability but also bolsters security and privacy.

**Work browser with a visual refresh:** The Microsoft Edge for Business icon, which replaces the existing Microsoft Edge icon in the taskbar and other shortcuts, provides a distinct and recognizable identity for the business browser.

**Enhanced security:** Microsoft Edge for Business fortifies the browsing experience by implementing app protection policies. These policies ensure that enterprise data remains secure, providing peace of mind for both the organization and its users.

**Centralized management:** Microsoft Intune offers centralized policy management for Microsoft Edge for Business that simplifies the process, saving time and resources.

In addition to the above benefits, you can enable protected Mobile Application Management access to corporate data on personal devices. This capability uses the following functionality:

- Intune application configuration policies (ACP) with Microsoft Edge for Business. Using ACP allows you to apply Microsoft Edge settings to better enable a secure browsing experience.
- Intune app protection policies to secure organization data and ensure the client device is healthy.
- Mobile Threat Protection (MTP) integrated with Intune app protection policies to detect local health threats on personal Windows and all mobile devices.
- Microsoft Entra Conditional Access to ensure the device is protected and healthy before granting protected services access via Microsoft Entra.

## Zero Trust Methodology

The [Zero Trust security strategy](/security/zero-trust/zero-trust-overview) is transforming the way organizations approach security. It’s becoming the new standard for security strategy in response to the evolving threat landscape. Traditional best practices revolved around the model of "trust but verify," however this approach is exploitable through modern attacks. This is driving the need for a shift in security strategy. The Zero Trust methodology is based on the concept of "never trust, always verify" and aligns with three key principles:

- **Verify Explicitly:** Always authenticate and authorize based on all available data points. These data points include user identity, location, device health, service/workload, data classification, and anomalies.
- **Use Least-Privilege Access:** Limit user access with just-in-time and just-enough-access (JIT/JEA) policies. Implement risk-based adaptive policies and data protection to secure both data and productivity.
- **Assume Breach:** Minimize the blast radius and segment access. Ensure end-to-end encryption and use analytics to gain visibility, drive threat detection, and improve defenses.

### Microsoft Edge for Business complements Zero Trust

Microsoft Edge for Business, built on the robust and secure foundation of Chromium, is designed to stay ahead of security threats. It releases updates and patches swiftly to counter threats such as zero-day exploits, minimizing the effect of any potential compromise.

In addition to the inherent security features of Chromium, Microsoft Edge for Business incorporates unique protection features and supports a range of Microsoft technologies:

- **[Microsoft Defender](/defender/):** Provides comprehensive security solutions.
- **[Microsoft Entra](/entra/):** Offers identity and access management services.
- **[Microsoft Intune](/mem/):** Offers mobile device and application management.
- **[Microsoft Purview](/purview/):** Supports data governance across your hybrid data estate.

Furthermore, Microsoft Edge for Business aligns with the Zero Trust methodology by offering the following features:

- **Data Loss Prevention (DLP) with Microsoft Purview:** Helps prevent data leaks and unauthorized data access.
- **Microsoft Defender SmartScreen:** Provides reputation-based protection against phishing and malware.
- **Enhanced Security Mode (ESM):** Offers extra security measures.
- **Website Typo Protection:** Helps prevent navigation to malicious sites due to typographical errors.
- **Native Support for Microsoft Entra Conditional Access:** Ensures only authenticated and authorized users can access your resources.
- **Password Monitoring and Generator:** Helps maintain strong, unique passwords.
- **Microsoft Edge Management Service (EMS):** Provides centralized control over your Microsoft Edge deployments.
- **Unmanaged Device Support with Microsoft Intune Mobile Application Management:** Allows secure access to enterprise resources from unmanaged devices.

## What's in this solution

This solution provides comprehensive guidance for implementing the Secure Enterprise Browser configuration using Microsoft Edge for Business and Microsoft Intune. The step-by-step approach covers all policy types and platforms, organized by configuration method to help you build a complete security framework.

Continue with [Step 1](mamedge-1-mamca.md) to create Microsoft Entra Conditional Access.
