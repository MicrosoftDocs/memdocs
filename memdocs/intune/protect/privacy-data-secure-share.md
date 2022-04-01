---
# required metadata

title: Data security and sharing in Intune
titleSuffix: Microsoft Intune
description: Learn how personal data is secured and shared in Intune.
keywords: privacy, data
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Data security and sharing in Intune


## Data security

Microsoft Intune is a key component of the Microsoft Enterprise Mobility and Security Suite cloud service offering. To support the [data governance strategy](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx), all Microsoft cloud services are developed with [Microsoft Privacy](https://www.microsoft.com/en-us/trustcenter/privacy) and [Microsoft Security](https://www.microsoft.com/en-us/trustcenter/security/) methodologies.  

Microsoft Intune follows the same technical and organizational measures that the Microsoft Azure service teams take for securing against data breach processes.

For more information, see the [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### Data breach reporting

When a Customer-Reportable Security Incident (CRSI) is identified, customers are notified. This process includes working with the Microsoft 365 team to communicate breach notification for any Microsoft 365 customers using Intune.

## Data sharing

When tenant admins turn on certain functionality (like the Apple Device Enrollment Program), Microsoft Intune obtains admin consent for sharing data with the appropriate third parties. In such cases, Intune may share personal data with:

- Third parties acting as Microsoft's agents.
- Third parties not acting as Microsoft's agents, but only when tenant admins explicitly grant Intune permission to do so.

All third parties acting as Microsoft agents are included in the [Online Services Subcontractor list](https://aka.ms/Online_Serv_Subcontractor_List).

Sharing data with such entities is done to aid customer and technical support, service maintenance, and other operations.

A tenant's contract with the third party governs the Intune personal data held in the third party's service. It also grants Intune the permission to transmit data to the third party service.  

For information about data shared with certain third parties, see the following articles:
- [Data Intune sends to Apple](data-intune-sends-to-apple.md)
- [Data Intune sends to Google](data-intune-sends-to-google.md)
- [Data Apple sends to Intune](data-apple-sends-to-intune.md)
- [Data Google sends to Intune](data-google-sends-to-intune.md)
- [Data Jamf Pro sends to Intune](data-jamf-sends-to-intune.md)

### Microsoft Endpoint Configuration Manager data sharing

Microsoft Intune does not share any data with Configuration Manager. Configuration Manager is an on-premise product deployed, managed, and operated directly by the customer. The diagnostics and usage data that is collected by Configuration Manager are only to improve the installation experience, quality, and security of future releases.

To learn more, see [Diagnostics and usage data for Configuration Manager](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data). 


## Next steps

Find out how to [view and correct](privacy-data-view-correct.md) personal data in Intune.
