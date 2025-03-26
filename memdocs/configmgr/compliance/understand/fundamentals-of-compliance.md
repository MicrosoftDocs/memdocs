---
title: Understand compliance in Configuration Manager
author: dougeby
ms.author: dougeby
manager: dougeby
audience: ITPro
ms.topic: concept-article
ms.service: configuration-manager
ms.collection: 
 - tier1
 - essentials-compliance
description: Learn about compliance certifications, dependencies, and features in Configuration Manager supporting data protection and regulatory requirements.
ms.date: 12/3/2024
---

# Understand compliance in Configuration Manager

Configuration Manager supports compliance features to help organizations meet national, regional, and industry-specific regulations. Configuration Manager aligns with Microsoft's commitment to data protection, privacy, and compliance, by offering tools to help secure and manage data effectively.

## Shared responsibility model

Microsoft ensures that Configuration Manager complies with various industry standards and regulatory frameworks. However, customers are responsible for implementing their data protection and compliance strategies to align with their specific organizational requirements.

## Compliance dependencies

Configuration Manager leverages other Microsoft services for compliance, including:

- [Microsoft Entra ID](/entra/fundamentals/whatis): Identity and access management.
- [Microsoft Intune](/mem/intune): Enforces device compliance and conditional access policies.

## Microsoft Intune capabilities for compliance

Microsoft Intune helps enforce compliance policies and protect organizational data specifically for Intune:

- **Conditional Access**: Ensures only compliant devices and apps managed by Intune can access sensitive data. See [Conditional Access](/mem/intune-service/protect/conditional-access).
- **Device Compliance Enforcement**: Enforces device compliance policies to meet organizational security requirements. See [Device Compliance Policies](/mem/intune-service/protect/device-compliance-get-started).

For more information about Intune compliance capabilities, visit the [Microsoft Intune documentation](/mem/intune).
> [!NOTE]
> For more information about how to concurrently manage Windows 10 or later devices by using both Configuration Manager and Microsoft Intune, see [What is co-management?](/mem/configmgr/comanage/overview).

## Data encryption

Use Configuration Manager to manage BitLocker Drive Encryption (BDE) for on-premises Windows clients, which are joined to Active Directory. It provides full BitLocker lifecycle management that can replace the use of Microsoft BitLocker Administration and Monitoring. For more information, see [Plan for BitLocker management](/mem/configmgr/protect/plan-design/bitlocker-management).

## Compliance features

Configuration Manager includes several compliance features that help organizations manage device compliance. For more information, see [Ensure device compliance with Configuration Manager](/mem/configmgr/compliance/understand/ensure-device-compliance).

## Related articles

- [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement)
- [Microsoft Trust Center](https://www.microsoft.com/trust-center)
- [Additional privacy information](/mem/configmgr/core/plan-design/security/additional-privacy)
- [Fundamentals of security](/mem/configmgr/core/understand/fundamentals-of-security)
