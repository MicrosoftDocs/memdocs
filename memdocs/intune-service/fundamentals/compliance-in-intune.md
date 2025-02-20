---
title: Compliance in Microsoft Intune
titleSuffix:
description: Learn about compliance, dependencies, and features in Microsoft Intune supporting data protection and regulatory requirements.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/03/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.collection: 
 - tier1
 - highpri
 - essentials-compliance

---

# Compliance in Microsoft Intune

Intune supports compliance features to help organizations meet national, regional, and industry-specific regulations. Intune aligns with Microsoft's commitment to data protection, privacy, and compliance by offering tools to help secure and manage data effectively.

## Shared responsibility model

Microsoft ensures that Intune complies with various industry standards and regulatory frameworks. However, customers are responsible for implementing their data protection and compliance strategies to align with their specific organizational requirements.

## Compliance certifications

Intune is covered under several compliance certifications, and regulatory standards. The following table provides a sample of the key certifications that are covered:

| Certification or Standard | Description | Applicability |
|---------------------------|-------------|---------------|
| [GDPR](/compliance/regulatory/gdpr) | EU General Data Protection Regulation for data privacy  | European Union |
| [ISO 27001](/compliance/regulatory/offering-iso-27001) | International standard for information security management | Global |
| [HIPAA](/compliance/regulatory/offering-hipaa-hitech)   | U.S. Health Insurance Portability and Accountability Act | United States |
| [SOC 2 Type 2](/compliance/regulatory/offering-soc-2)  | Service Organization Controls for data security | Global |

> [!NOTE]
> Microsoft Intune helps your organization meet regulatory compliance standards. Intune supports additional certifications, such as [ISO 22301](/compliance/regulatory/offering-iso-22301), [ISO/IEC 27017](/compliance/regulatory/offering-iso-27017), [ISO/IEC 27018](/compliance/regulatory/offering-iso-27018), [ISO/IEC 27701](/compliance/regulatory/offering-iso-27701), [SOC 1 Type 2](/compliance/regulatory/offering-soc-1), [SOC 3](/compliance/regulatory/offering-soc-3), and [WCAG](/compliance/regulatory/offering-wcag-2-1).

For a complete list, see [Microsoft compliance offerings](/compliance/regulatory/offering-home).

## Compliance dependencies

Intune leverages other Microsoft services for compliance, including:

- [Microsoft Purview](/purview/purview): A suite of data governance and compliance tools.
- [Microsoft Entra ID](/entra/fundamentals/whatis): Identity and access management, formerly known as Azure Active Directory (Azure AD).
- [Microsoft Purview Compliance Manager](/purview/compliance-manager): Tools for managing compliance across your organization.
- [Microsoft Defender for Endpoint](../protect/advanced-threat-protection.md): An enterprise endpoint security platform.

## Microsoft Intune capabilities for compliance

Microsoft Intune helps enforce compliance policies and protect organizational data specifically for Intune:

- **Conditional Access**: Ensures only compliant devices and apps managed by Intune can access sensitive data. See [Conditional Access](/mem/intune-service/protect/conditional-access).
- **Device Compliance Enforcement**: Enforces device compliance policies to meet organizational security requirements. See [Device Compliance Policies](/mem/intune-service/protect/device-compliance-get-started).

For more information about Intune compliance capabilities, visit the [Microsoft Intune documentation](/mem/intune).

## Data residency and protection

Intune supports compliance with data residency requirements by supporting Microsoft Cloud's regional and global data storage policies. These policies include:

- **Data location**: Data is stored in Microsoft-managed data centers. For more information, see [Data storage and processing in Intune](../protect/privacy-data-store-process.md).
- **EU Data Boundary**: Ensures that data belonging to EU customers is stored and processed within the EU. For more information, see [EU Data Boundary](/privacy/eudb/eu-data-boundary-learn) and [Configure Microsoft Tunnel for Intune](../protect/microsoft-tunnel-configure.md).
- **Encryption**: Data is encrypted at rest and in transit. For more information, see [Access requirements policy mapping from Basic Mobility and Security to Intune](../fundamentals/policy-map-access-requirements.md).

## Compliance features

Intune includes several compliance features that help organizations meet regulatory requirements, manage data lifecycles, and protect sensitive information. These features are designed to ensure your organization can effectively monitor, classify, and safeguard its data while maintaining compliance with industry standards.

### Data lifecycle management

> [!IMPORTANT]
> Microsoft Intune doesn't use any personal data collected as part of providing the service for profiling, advertising, or marketing purposes. 

Intune supports data lifecycle management through retention policies and labels. These features help organizations retain or delete data based on compliance requirements. For more information, see [Privacy and personal data in Intune](../fundamentals/intune-service-servicing-information.md#privacy-and-personal-data-in-intune).

### Auditing and reporting

Microsoft Purview (included in the **Microsoft 365 E5** license) supports auditing and reporting for Intune. IT administrators can monitor data usage and ensure adherence to organizational compliance policies. Features include:

- eDiscovery: Enables organizations to locate data for legal or regulatory needs.
- Data Retention Policies: Helps organizations manage data lifecycles.

For more information, see the [Protect your sensitive data with Microsoft Purview](/purview/information-protection).

### Privacy controls

Intune includes privacy controls to manage data collection, storage, and sharing:

For details about privacy, see [Privacy and personal data in Intune](../protect/privacy-personal-data.md).

## Related articles

- [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement)
- [Microsoft Trust Center](https://www.microsoft.com/trust-center)
- [Microsoft Purview compliance portal](https://compliance.microsoft.com/)