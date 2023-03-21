---
# required metadata

title: Zero Trust with Microsoft Intune
description: Microsoft Intune contributes to a strong Zero Trust strategy and architecture.
keywords: Zero Trust, security architecture, security strategy, cyber security, enterprise security, devices, device, identity, users, data, applications
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 03/21/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
- zerotrust-services
---

# Zero Trust with Microsoft Intune

[Zero Trust](/security/zero-trust/zero-trust-overview) is a security strategy for designing and implementing the following set of security principles:

| Verify explicitly  | Use least privilege access | Assume breach |
|---------|---------|---------|
| Always authenticate and authorize based on all available data points. | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

## Device and application authentication, authorization, and protection for Zero Trust

You can use Intune to protect access and data on organization-owned and user's personal devices and has compliance and reporting features that support Zero Trust.

| Zero Trust principle | How Intune helps |
|---------|---------|
| Verify explicitly | Intune allows you to configure policies for apps, security settings, device configuration, compliance, Azure Active Directory (AD) Conditional Access, and more. These policies become part of the authentication and authorization process of accessing resources.  |
| Use least privilege access | Intune simplifies app management with a built-in app experience, including app deployment, updates, and removal. You can connect to and distribute apps from your private app stores, enable Microsoft 365 apps, deploy Win32 apps, create app protection policies, and manage access to apps and their data. |
| Assume breach | Intune integrates with mobile threat defense services, including Microsoft Defender for Endpoint and third party partner services. With these services, you can create policies for endpoint protection that respond to threats, do real-time risk analysis, and automate remediation. |

## Next steps

Learn more about Zero Trust and how to build an enterprise-scale strategy and architecture with the [Zero Trust Guidance Center](/security/zero-trust).

For device-centric concepts and deployment objectives, see [Secure endpoints with Zero Trust](/security/zero-trust/deploy/endpoints)

For Intune in Microsoft 365, see [Manage devices with Intune Overview](/microsoft-365/solutions/manage-devices-with-intune-overview).

Learn more about other Microsoft 365 capabilities that contribute to a strong Zero Trust strategy and architecture with [Zero Trust deployment plan with Microsoft 365](/microsoft-365/security/microsoft-365-zero-trust).

