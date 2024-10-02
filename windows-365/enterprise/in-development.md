---
# required metadata

title: In development - Windows 365 Enterprise
description: Windows 365 Enterprise features in development
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/02/2024
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
ms.subservice: windows-365-enterprise
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

### Cloud PC gallery images update to Microsoft Teams 2.1<!--50394023-->

In a future update, Windows 365 Cloud PC gallery images with Microsoft 365 applications will be updated to use Microsoft Teams 2.1. These images include:

- Windows 11 Enterprise + Microsoft 365 Apps  21H2
- Windows 10 Enterprise + Microsoft 365 Apps 22H2
- Windows 10 Enterprise + Microsoft 365 Apps 21H2

### Azure network connections inactive state<!--52127015-->

In a future update, Azure network connections that meet either of the following conditions for more than four weeks will be marked as inactive:

- ANCs that aren't associated with provisioning policies.
- ANCs with provisioning policies that have no Cloud PCs associate with them.

Inactive ANCs:

- Can't be assigned to provisioning policies.
- Are skipped during health checks.

You'll be able to reactive such ANCs.

<!-- ***********************************************-->
<!--## Device security-->

<!--***********************************************-->
<!-- ## End user experience -->

<!-- ***********************************************-->
<!--## Miscellaneous
-->

<!-- ***********************************************-->
## Monitor and troubleshoot

### End user manual connectivity check<!--37679345 -->

End users will be able to manually run connectivity checks on their Cloud PCs from [windows365.microsoft.com](https://windows365.microsoft.com).

### Update to Cloud PC action status report<!--49451077-->

The Cloud PC action status report will show batches of devices in which actions have been triggered. Customers will be able to see the batch current progress.

### Remoting connections report deprecation<!--52990648-->

The remoting connection report will be retired on December 31st, 2024. After this date, refer to the [Cloud PC connection quality report](report-cloud-pc-connection-quality.md).

<!-- ***********************************************-->
<!--## Provisioning-->

<!-- ***********************************************-->
<!--## Security-->

<!-- ***********************************************
## Windows 365 app-->

<!-- ***********************************************-->
<!--## Windows 365 Frontline-->


## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
