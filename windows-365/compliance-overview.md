---
title: Compliance in Windows 365
author: erikjeMS
ms.author: erikje
manager: dougeby
audience: ITPro
ms.topic: conceptual
ms.service: windows-365
ms.collection: 
 - tier1
 - essentials-compliance
ms.localizationpriority: medium
description: Learn about compliance certifications, dependencies, and features in Windows 365 supporting data protection and regulatory requirements.
ms.date: 12/9/2024
---

# Compliance in Windows 365

Windows 365 supports compliance features to help organizations meet national, regional, and industry-specific regulations. Windows 365 align with Microsoft's commitment to data protection, privacy, and compliance, offering tools to help secure and manage data effectively.

## Shared responsibility model

Microsoft ensures that Windows 365 complies with various industry standards and regulatory frameworks. However, customers are responsible for implementing their data protection and compliance strategies to align with their specific organizational requirements.

## Compliance certifications

Windows 365 are covered under several compliance certifications and regulatory standards. The following table provides a sample of the key certifications that are covered:

| Certification or Standard | Description | Applicability |
|---------------------------|-------------|---------------|
| [GDPR](/compliance/regulatory/gdpr) | EU General Data Protection Regulation for data privacy  | European Union |
| [ISO 27001](/compliance/regulatory/offering-iso-27001) | International standard for information security management | Global |
| [HIPAA](/compliance/regulatory/offering-hipaa-hitech)   | U.S. Health Insurance Portability and Accountability Act | United States |

> [!NOTE]
> Windows 365 helps your organization meet regulatory compliance standards. Windows 365 supports additional certifications, such as [ISO 22301](/compliance/regulatory/offering-iso-22301), [ISO/IEC 27017](/compliance/regulatory/offering-iso-27017), [ISO/IEC 27018](/compliance/regulatory/offering-iso-27018), and [ISO/IEC 27701](/compliance/regulatory/offering-iso-27701). 

For additional certifications, visit [Microsoft Compliance Offerings](/compliance/regulatory/offering-home).

## Compliance dependencies

Windows 365 leverages other Microsoft services for compliance, including:

- [Microsoft Purview](/purview/purview): A suite of data governance and compliance tools.
- [Microsoft Entra ID](/entra/fundamentals/whatis): Identity and access management, formerly known as Azure Active Directory (Azure AD).
- [Microsoft Purview Compliance Manager](/purview/compliance-manager): Tools for managing compliance across your organization.
- [Microsoft Intune](/mem): Enforces device compliance and Conditional Access policies to protect access to Windows 365 Cloud PCs.

## Microsoft Intune capabilities for compliance

Microsoft Intune helps enforce compliance policies and protect organizational data specifically for Windows 365:

- **Conditional Access**: Ensures only compliant devices running Windows 365 can access sensitive data. See [Conditional Access](/mem/intune/protect/conditional-access).
- **Device Compliance Enforcement**: Enforces device compliance policies to meet organizational security requirements. See [Device Compliance Policies](/mem/intune/protect/device-compliance-get-started).

For more information about Intune compliance capabilities, visit the [Microsoft Intune documentation](/mem).

## Data location and encryption

Windows 365 supports compliance with data residency requirements by supporting Microsoft Cloud's regional and global data storage policies. These policies include:

- Data location: Data is stored in Microsoft-managed data centers. For more information, see [Windows 365 data storage](enterprise/privacy-personal-data.md#windows-365-data-storage).
- Encryption: Data is encrypted at rest and in transit. For more information, see [Data encryption in Windows 365](enterprise/encryption.md).

## Compliance features

Windows 365 includes several compliance features that help organizations meet regulatory requirements, manage data lifecycles, and protect sensitive information. These features are designed to ensure your organization can effectively monitor, classify, and safeguard its data while maintaining compliance with industry standards.

### Data lifecycle management

Windows 365 supports data lifecycle management through retention policies and labels. These features help organizations retain or delete data based on compliance requirements. For setup instructions, see [How long is customer data and customer content stored?](enterprise/privacy-personal-data.md#how-long-is-customer-data-and-customer-content-stored)

### Auditing and reporting

Microsoft Purview supports auditing and reporting for Windows 365. IT administrators can monitor data usage and ensure adherence to organizational compliance policies. For more information, visit the [Microsoft Purview Customer Key for Windows 365 Cloud PCs](enterprise/purview-customer-key.md).

### Privacy controls

Windows 365 includes privacy controls to manage data collection, storage, and sharing:

For details about privacy, see [Privacy, customer data, and customer content in Windows 365](enterprise/privacy-personal-data.md).

## Related articles

- [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement)
- [Microsoft Trust Center](https://www.microsoft.com/trust-center)
- [Microsoft Purview compliance portal](https://compliance.microsoft.com/)
