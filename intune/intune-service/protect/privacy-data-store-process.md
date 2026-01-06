---
title: Data storage and processing in Intune
description: Learn how personal data is stored and processed in Intune.
author: paolomatarazzo
ms.author: paoloma
ms.date: 06/25/2025
ms.topic: article
ms.reviewer: bradyw
ms.collection:
- M365-identity-device-management
- privacy
- sub-data-privacy
---

# Data storage and processing in Intune


### Storage locations

Microsoft Intune isn't deployed to all Microsoft data centers globally. We make decisions on where to deploy Intune services based on the number of customers, regional affiliations, and to help customers comply with laws, regulations or industry standards that explicitly govern the location of data storage.

Microsoft offers and operates Intune services in three major geographic regions:

- **North America** - Includes data centers in the United States
- **Europe** - Includes data centers located solely in the [European Data boundary](/privacy/eudb/eu-data-boundary-learn): European Union (EU) and the European Free Trade Association (EFTA)
- **Asia Pacific** - Includes data centers in Australia, Hong Kong Special Administrative Region, India, Japan, Singapore, and South Korea

Intune is also available in the following local geographies:

- **Australia**
- **India**
- **Switzerland**

When a customer first provisions Intune, the tenant's Customer Data is hosted in the geography that best aligns with the country/region value in its Microsoft Entra directory. This value is set as part of the Microsoft Entra directory creation process and can't be modified later.

For existing tenants, refer to endpoint.microsoft.com, Tenant Administration | Tenant Status. If you don't have an existing tenant, create a trial tenant and provision Intune.

Over time, Intune may be deployed to additional geographies, so the provisioning locations for new customers can change over time. For existing tenants, this doesn't cause customer data to move to a new geography.

Microsoft Intune won't store Customer Data at rest outside the stated geo, except if:

- It's necessary for Microsoft to provide customer support, troubleshoot the service, or comply with legal requirements.
- The customer configures an account to enable such storage of customer data, including by using the following:
  - Features that are designed to operate globally, such as Content Delivery Network (CDN), which provides a global caching service and stores customer data at edge locations around the world.
  - If you are using Intune's enrollment and compliance notification features to send emails to end-users, the emails will be processed within the respective country for sovereign cloud customers, in EMEA for customers located in EMEA, and in North America for all other customers.
- For Microsoft Entra ID: Refer to [Microsoft Entra Data Locations](https://aka.ms/aaddatamap).
- Preview, beta, or other prerelease services, which typically store customer data in the United States but might store it globally.

Microsoft doesn't control or limit the Geo from which customers or their end users might access customer data. Similarly, where customer data in other services is subsequently integrated into Intune, the originating customer data will continue to be stored subject to the other service's own Geo commitments (if any); only the copy of the customer data integrated into Intune will be stored in the stated Geo for Intune.

### Data residency option

Data residency is important for government, public sector, education and regulated commercial entities to help ensure protection of personal and/or sensitive information. In many countries/regions, customers are expected to comply with laws, regulations or industry standards that explicitly govern the location of data storage.

Towards this end, we offer existing customers an option to request migration of their organization's Customer Data at rest to the datacenter geography that matches their signup Country or region.

With this option, eligible customers with data residency requirements can request migration of their organization's Customer Data at rest to the geography that best aligns with  their  Entra directory country/region value, when available, if minimal data loss and reconfiguration is acceptable. Microsoft offers a committed deadline to all eligible customers who request migration. [Contact support](../../get-support.md) to request your data move. Our support team will guide you through the preparation steps that you need to take and limitations you should be aware of. Data moves can take up to 24 months after the request period ends to complete.

During migration, certain features might not be accessible. The actual down time and impact to end-users depends on the volume of data to be migrated and features in use. When migration is complete, the support team will contact you to make sure everything is working.

Data moves to the new datacenter geographies are completed at no extra cost to the customer.


### Personal data retention

Microsoft 365 Data Handling Standard policy specifies how long customer data is retained after deletion. There are two scenarios in which customer data is deleted:

-**Active Deletion**: The tenant has an active subscription and a user or administrator deletes data, or administrators delete a user.
-**Passive Deletion**: The tenant subscription ends.

For each of the deletion scenarios, see [Data Retention, Deletion, and Destruction in Microsoft 365](/microsoft-365/enterprise/microsoft-365-data-retention-deletion-and-destruction-overview?view=o365-worldwide&preserve-view=true).

In general, personal data collected by Intune is removed within 30 days after deletion. Audit logs are retained for up to two year for security purposes.

## Processing personal data

Intune processes personal data with ISO certified systems. For more information, see the [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### Profiling and marketing

Microsoft Intune doesn't use any personal data collected as part of providing the service for profiling or marketing purposes.

## Next steps

Find out more about how Intune [secures and shares](privacy-data-secure-share.md) personal data.
