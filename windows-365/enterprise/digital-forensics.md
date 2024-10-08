---
# required metadata
title: Digital forensics with Windows 365 Enterprise Cloud PCs
titleSuffix:
description: Learn about using Windows 365 Enterprise Cloud PCs with digital forensics.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/28/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: anbiswas    
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Digital forensics and Windows 365 Enterprise Cloud PCs

Just like physical devices, Windows 365 Enterprise Cloud PCs can be deployed, secured, and managed using [Microsoft Intune](/mem/intune/fundamentals/what-is-intune). As part of PC ownership, you may be asked to submit Cloud PCs to internal or third parties to perform digital forensics. Digital forensics is the science that addresses the recovery and investigation of digital data to support criminal investigations or civil proceedings.

To support these forensics, Windows 365 offers the ability to [place a Cloud PC under review](place-cloud-pc-under-review.md). This action will securely save a snapshot of the Cloud PC to the customer’s Azure Storage Account. When transferred to that account, the customer has complete ownership of the snapshot. To make the snapshot tamper-evident, the customer should create a file hash of the snapshot as soon as the snapshot has been saved in the Azure Storage account.

Investigators can attach disk copies of the Cloud PC snapshot and transfer it to a secure storage account dedicated to forensic analysis. This process can be done without re-creating, powering on, or accessing the original source Cloud PC.

## Scenarios

You may have to place a Cloud PC under review for any of these scenarios:

1. A request from an internal Security Operation Center (SOC) team.
2. A response to a request from an internal or external third party auditor.
3. As a response to a pending or ongoing legal investigation.

## Considerations for digital forensics

In response to legal requests for data stored on a Cloud PC, admins must attest that digital evidence they provide demonstrates a valid Chain of Custody (CoC) throughout the evidence acquisition, preservation, and access process. For this reason, admins should make sure to support adequate:

- access control
- data protection and integrity
- monitoring and alerting
- logging and auditing

<!-- ########################## -->
## Next steps

[Place a Cloud PC under review](place-cloud-pc-under-review.md).

For more information about Microsoft’s support for digital investigations, see [Computer forensics chain of custody in Azure]( /azure/architecture/example-scenario/forensics/).
