---
# required metadata

title: Data storage and processing in Intune
titleSuffix: Microsoft Intune
description: Learn how personal data is stored and processed in Intune.
keywords: data, privacy
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8

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

# Data storage and processing in Intune

### Storing customer data

After Intune [collects the data](privacy-data-collect.md), Intune follows the Data Handling Standard policy for Microsoft 365 that specifies how customer data is stored and processed. See [Where your Microsoft 365 customer data is stored](/microsoft-365/enterprise/o365-data-locations). Personal data is processed within the audited compliance boundary of the Intune service under the technical security measures assured through [Microsoft Online Services Terms (OST)](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

### Storage locations

Microsoft offers and operates Intune services in many regions worldwide. Intune respects the storage location elections made by the administrator for Customer Data.

For more information, see [Data Center Locations](/microsoft-365/enterprise/o365-data-locations?view=o365-worldwide#data-center-locations)

### Data residency option

We open new datacenter geographies for Intune to add capacity and compute resources to support our ongoing customer demand and usage growth. Additionally, the new datacenter geographies offer in-region data residency for Customer Data. 

Existing customers that have their Customer Data stored in an already existing datacenter geography are not impacted by the launch of a new datacenter geography. We introduce no unique capabilities, features, or compliance certifications with the new datacenter geography. As a customer, you will experience the same quality of service, performance, and security controls in any of those two geographies. 

We offer existing customers an option to request migration of their organization's Customer Data at rest to the datacenter geography that matches their signup Country or region. 

With this option, eligible customers with data residency requirements can request migration of their organization's Customer Data at rest to their new datacenter geography if minimal data loss and reconfiguration is acceptable. Microsoft will offer a committed deadline to all eligible customers who request migration. [Contact support](../../get-support.md) to request your data move. Our support team will guide you through the preparation steps you’ll need to take and limitations you should be aware of. Data moves can take up to 24 months after the request period ends to complete.

During migration, certain features may not be accessible. The actual down time and impact to end-users depends on the volume of data to be migrated and features in use. When migration is complete, support will contact you to make sure everything is working.

Data moves to the new datacenter geo are completed at no additional cost to the customer.


### Personal data retention

Microsoft 365 Data Handling Standard policy specifies how long customer data is retained after deletion. There are two scenarios in which customer data is deleted:

-**Active Deletion**: The tenant has an active subscription and a user or administrator deletes data, or administrators delete a user.
-**Passive Deletion**: The tenant subscription ends.

For each of the deletion scenarios, see [Data Retention, Deletion, and Destruction in Microsoft 365](/microsoft-365/enterprise/microsoft-365-data-retention-deletion-and-destruction-overview?view=o365-worldwide).  

In general, personal data collected by Intune is removed within 30 days after deletion. Audit logs are retained for up to one year for security purposes. 


## Processing personal data

Intune processes personal data with ISO certified systems. For more information, see the [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### Profiling and marketing

Microsoft Intune does not use any personal data collected as part of providing the service for profiling or marketing purposes. 

## Next steps

Find out more about how Intune [secures and shares](privacy-data-secure-share.md) personal data.
