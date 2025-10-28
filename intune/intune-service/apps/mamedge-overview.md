---
title: Secure Your Corporate Data Using Microsoft Edge for Business
description: Secure your corporate data in Microsoft Intune with Microsoft Edge for Business across all platforms.
ms.date: 10/28/2025
ms.topic: overview
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Secure Your Corporate Data in Intune With Microsoft Edge for Business

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

## Overview

This guide provides comprehensive step-by-step instructions to implement the Secure Enterprise Browser experience using the data protection framework:

1. **[Microsoft Entra Conditional Access with Microsoft Edge for Business](mamedge-1-mamca.md)** - Create Microsoft Entra Conditional Access policies and Intune app protection policies for browsing on Android, iOS, and Windows.
2. **[App protection policies for Microsoft Edge for Business](mamedge-2-app.md)** - Implement Level 1, Level 2, and Level 3 app protection policies for Windows, Android, and iOS platforms to ensure secure access and usage of enterprise applications.
3. **[Integrate Mobile Threat Defense](mamedge-3-scc.md)** - Enhance the overall security posture of your organization by integrating the secure enterprise browser with Windows Security Center, Microsoft Defender, or MTD partners.
4. **[App configuration policies for Microsoft Edge for Business](mamedge-4-acp-edge.md)** - Configure Level 1, Level 2, and Level 3 app configuration policies for Android, iOS, and Windows to customize browser behavior and features.
5. **[Settings catalog for Microsoft Edge for Business](mamedge-5-settings-catalog.md)** - Apply Level 1, Level 2, and Level 3 settings catalog configurations for Windows and macOS to establish comprehensive device-level browser controls.
6. **[Security baseline for Microsoft Edge](mamedge-6-security-baseline.md)** - Deploy the Microsoft Edge security baseline to rapidly implement Level 2 security with 23 preconfigured settings.
7. **[Microsoft Edge for Business end user experience](mamedge-7-end-user-experience.md)** - Understand how security measures affecting user interaction for Microsoft Edge for Business.
8. **[Troubleshooting and FAQ](mamedge-8-troubleshoot.md)** - Troubleshoot app protection policies with validation examples and frequently asked questions.

For more information about Microsoft Edge Security content, see [Microsoft Edge for Business: AI and protection in one secure enterprise browser](https://aka.ms/EdgeSecuritywhitepaper).

## Secure Enterprise Browser

The Secure Enterprise Browser solution combines Microsoft Edge for Business with Microsoft Intune's comprehensive policy framework to create a secure, manageable browsing experience across all platforms. This solution extends the proven data protection framework beyond app protection policies to include app configuration policies and settings catalog configurations, providing a unified approach to securing enterprise browser deployments.

### Data Protection Framework for Secure Enterprise Browser

The data protection framework for the Secure Enterprise Browser builds on the established app protection policy framework and extends it to encompass all configuration aspects of Microsoft Edge for Business. This framework organizes security configurations into three levels:

- **Level 1 - Enterprise basic data protection**: The minimum recommended configuration for enterprise devices. This level provides fundamental security controls while maintaining user productivity.
- **Level 2 - Enterprise enhanced data protection**: Recommended for devices accessing sensitive or confidential information. This configuration applies to most users accessing work or school data and includes extra controls that might affect user experience.
- **Level 3 - Enterprise high data protection**: Designed for organizations with sophisticated security requirements or users at elevated risk. This configuration provides the highest level of protection for sensitive data.

Each level applies consistently across app protection policies, app configuration policies, and settings catalog configurations, allowing you to implement a cohesive security strategy tailored to your organization's needs.

### What is Microsoft Edge for Business?

Microsoft Edge for Business is a dedicated Microsoft Edge browsing experience designed specifically for work environments. Microsoft Edge for Business is secure by default. It enables admins in organizations to give their users a productive and secure work-browser provided across managed and unmanaged devices. In addition, Microsoft Edge for Business has the same rich set of enterprise controls, security, and productivity features that you're already familiar with in Microsoft Edge, and it's built to help meet the evolving needs of businesses and organizations.

Microsoft Edge for Business aims to address the needs of both end users and IT Pros by automatically separating work and personal browsing. Microsoft Edge for Business does this using dedicated browser windows containing their own favorites, separate caches, and storage locations. This separation ensures that work related content doesn't get intermingled with personal browsing. In addition, it helps to prevent end users accidentally share sensitive information with unintended audiences.

### Is this a new browser?

No, this isn’t a new browser. This is a new, dedicated Microsoft Edge experience built specifically for work. It allows organizations to configure it to maximize productivity and security. It retains the same functionality that users are already familiar with in Microsoft Edge. Additionally, it offers an optional feature of automatic switching between personal and corporate accounts, designed to meet the evolving needs of users and businesses. Signing in with a Microsoft Entra ID will automatically enable the Microsoft Edge for Business experience. 

### Benefits

Microsoft Edge for Business offers a multitude of advantages:

**Streamlined IT operations:** Microsoft Edge for Business can significantly reduce the cyber-attack surface area and enhance your organization’s security posture. It achieves this by streamlining down operations to a single browser for all use cases, simplifying IT management.

**Improved user experience:** For end users signed in with both work and personal profiles, Microsoft Edge for Business offers a superior browsing experience. The automatic switching feature not only enhances usability but also bolsters security and privacy.

**Work browser with a visual refresh:** The Microsoft Edge for Business icon, which replaces the existing Microsoft Edge icon in the taskbar and other shortcuts, provides a distinct and recognizable identity for the business browser.

**Enhanced security:** Microsoft Edge for Business fortifies the browsing experience by implementing app protection policies. These policies ensure that enterprise data remains secure, providing peace of mind for both the organization and its users.

**Centralized management:** With Microsoft Intune, managing a Microsoft Edge for Business policy experience isn't complex. This centralized management system simplifies the process, saving time and resources.

In addition to the above benefits, you can enable protected Mobile Application Management access to corporate data on personal devices. This capability uses the following functionality:
- Intune application configuration policies (ACP) with Microsoft Edge for Business. Using ACP allows you to apply Microsoft Edge settings to better enable a secure browsing experience.
- Intune app protection policies to secure organization data and ensure the client device is healthy.
- Mobile Threat Protection (MTP) integrated with Intune APP to detect local health threats on personal Windows and all mobile devices.
- Microsoft Entra Conditional Access to ensure the device is protected and healthy before granting protected services access via Microsoft Entra.

## Zero Trust Methodology

The [Zero Trust security strategy](/security/zero-trust/zero-trust-overview) is transforming the way organizations approach security. It’s becoming the new standard for security strategy in response to the evolving threat landscape. Traditional best practices revolved around the model of "trust but verify," however this approach is exploitable through modern attacks. This is driving the need for a shift in security strategy. The Zero Trust methodology is based on the concept of "never trust, always verify" and aligns with three key principles:

- **Verify Explicitly:** Always authenticate and authorize based on all available data points. These data points include user identity, location, device health, service/workload, data classification, and anomalies.
- **Use Least-Privilege Access:** Limit user access with just-in-time and just-enough-access (JIT/JEA) policies. Implement risk-based adaptive policies and data protection to secure both data and productivity.
- **Assume Breach:** Minimize the blast radius and segment access. Ensure end-to-end encryption and use analytics to gain visibility, drive threat detection, and improve defenses.

### Microsoft Edge for Business complements Zero Trust

Microsoft Edge for Business, built on the robust and secure foundation of Chromium, is designed to stay ahead of security threats. It releases updates and patches swiftly to counter threats such as zero-day exploits, minimizing the effect of any potential compromise.

In addition to the inherent security features of Chromium, Microsoft Edge for Business incorporates unique protection features and supports a range of Microsoft technologies:

- **Microsoft Defender:** Provides comprehensive security solutions.
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

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps.png" alt-text="Steps to secure your corporate data in Intune with Microsoft Edge for Business.":::](mamedge-1-mamca.md)

Continue with [Step 1](mamedge-1-mamca.md) to create Microsoft Entra Conditional Access.
