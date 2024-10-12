---
# required metadata

title: Zero Trust with Microsoft Intune
description: Microsoft Intune contributes to a strong Zero Trust strategy and architecture.
keywords: Zero Trust, security architecture, security strategy, cyber security, enterprise security, devices, device, identity, users, data, applications
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/13/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
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

You can use Intune to protect access and data on organization-owned and user's personal devices and have compliance and reporting features that support Zero Trust.

| Zero Trust principle | How Intune helps |
|---------|---------|
| Verify explicitly | Intune allows you to configure policies for apps, security settings, device configuration, compliance, Microsoft Entra Conditional Access, and more. These policies become part of the authentication and authorization process of accessing resources. |
| Use least privilege access | Intune simplifies app management with a built-in app experience, including app deployment, updates, and removal. You can connect to and distribute apps from your private app stores, enable Microsoft 365 apps, deploy Win32 apps, create app protection policies, and manage access to apps and their data. </br></br>  With [Endpoint Privilege Management (EPM)](../protect/epm-overview.md), you can run your organization’s users as standard users (without administrator rights) while enabling those same users to complete tasks that require elevated privileges.  </br></br> [Intune policy for Windows Local Administrator Password Solution](../protect/windows-laps-overview.md) (LAPS) can help you to secure the local administrator account on Windows devices. Because the local admin account can’t be deleted and has full permissions to the device, being able to manage the built-in Windows administrator account is an important step in securing your organization. |
| Assume breach | Intune integrates with mobile threat defense services, including Microsoft Defender for Endpoint and third party partner services. With these services, you can create policies for endpoint protection that respond to threats, do real-time risk analysis, and automate remediation. |

## Next steps

Learn more about Zero Trust and how to build an enterprise-scale strategy and architecture with the [Zero Trust Guidance Center](/security/zero-trust).

For device-centric concepts and deployment objectives, see [Secure endpoints with Zero Trust](/security/zero-trust/deploy/endpoints).

For Intune in Microsoft 365, see [Manage devices with Intune Overview](/microsoft-365/solutions/manage-devices-with-intune-overview).

Learn more about other Microsoft 365 capabilities that contribute to a strong Zero Trust strategy and architecture with [Zero Trust deployment plan with Microsoft 365](/microsoft-365/security/microsoft-365-zero-trust).
