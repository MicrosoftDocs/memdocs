---
# required metadata

title: In development - Windows 365 Enterprise
description: Windows 365 Enterprise features in development
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2024
ms.topic: conceptual
ms.service: windows-365

# optional metadata

#audience:

ms.reviewer: traceyadams
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: references_regions
ms.collection:
- M365-identity-device-management
- tier2
---

# In development for Windows 365 Enterprise

To help in your readiness and planning, this page lists Windows 365 updates and features that are in development but not yet released. In addition to the information on this page:

- If we anticipate that you need to take action before a change, we publish a complementary post in Office message center.
- When a feature enters production, the feature description moves from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for more updates.
- Similar features might be announced at different times for Windows 365 Business.

> [!NOTE]
> This page reflects our current expectations about Windows 365 capabilities in an upcoming release. Dates and individual features might change. This page doesn't describe all features in development.

**This article was last updated on the date listed under the title above.**

<!-- Common categories:  
## App management
## Device configuration
## Device provisioning
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security
## End-user experience

-->

<!-- ***********************************************-->
## Device management

### Support for symmetric NAT with RDP Shortpath<!--43602619-->

In a future update, RDP Shortpath in Windows 365 will support establishing an indirect UDP connection using Traversal Using Relays around NAT (TURN) for symmetric NAT.  TURN is a popular standard for device-to-device networking for low latency, high-throughput data transmission with Azure Communication Services. For more information about TURN and Azure Communication Services, see [Network Traversal Concepts](/azure/communication-services/concepts/network-traversal). For more information about RDP Shortpath, see [Use RDP Shortpath for public networks with Windows 365](rdp-shortpath-public-networks.md).

### Chroma subsampling default change to 4:2:0<!--50308895-->

To reduce monitor support issues, the Windows 365 service will default the chroma subsampling at 4:2:0 (instead of the previous 4:4:4).

<!-- ***********************************************-->
## Device security

### Windows 365 Government support for Customer Lockbox<!--48802385-->

Windows 365 Government will support Microsoft Purview Customer Lockbox.

For more information, see [Microsoft Purview Customer Lockbox](/purview/customer-lockbox-requests).

<!--***********************************************-->
<!-- ## End user experience -->

<!-- ***********************************************-->
## Miscellaneous

### Upgrade Windows 365 licenses in Microsoft admin center<!--45415383-->

In a future update, customers that have Modern Microsoft Cloud Agreements will be able to upgrade their existing Windows 365 licenses in the Microsoft Admin Center.

### New Windows 365 Frontline offers for GCC<!--50308895-->

New Windows 365 Frontline offers will be available for Government Community Cloud (GCC) customers using the Azure Commercial cloud.

<!-- ***********************************************-->
## Monitor and troubleshoot

### End user manual connectivity check<!--37679345 -->

End users will be able to manually run connectivity checks on their Cloud PCs from [windows365.microsoft.com](https://windows365.microsoft.com).

### Windows 365 Government support for Cloud PC utilization report<!--49200860-->

Windows 365 Government will support the Cloud PC utilization report.

For more information, see [Cloud PC utilization report](report-cloud-pc-utilization.md).

### Update to Cloud PC action status report<!--49451077-->

The Cloud PC action status report will show batches of devices in which actions have been triggered. Customers will be able to see the batch current progress.

<!-- ***********************************************-->
## Provisioning

### New health check: UDP TURN (preview)<!--44505391-->

A new UDP TURN check will be added to the Azure Network Connections health checks. For more information about health checks, see [Azure network connections health checks](health-checks.md).


### New Cloud PC images aligned with Microsoft 365 apps images<!--48537480-->

In a future update, new Cloud PC optimized images aligned with the Microsoft 365 apps images will be available in the gallery.

<!-- ***********************************************-->
## Security

### FQDN requirement changes<!--46731885-->

In a future update, Windows 365 will remove a large number of FQDNs from the current published list and move them to the existing *.infra.windows365.microsoft.com wildcard FQDN. This change will reduce the initial configuration requirements and the change rate of connectivity requirements. For Windows 365 Government, the FQDNs will be moved to *.infra.windows365.microsoft.us.

### New settings for Windows 365 security baselines<!--49685126-->

New configuration settings will be introduced for the Windows 365 security baseline.

<!-- ***********************************************
## Windows 365 app-->

<!-- ***********************************************-->
<!--## Windows 365 Frontline-->


## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
