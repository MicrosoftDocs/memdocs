---
# required metadata

title: In development - Windows 365 Enterprise
titleSuffix: 
description: Windows 365 Enterprise features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 09/14/2022
ms.topic: reference
ms.service: cloudpc
ms.subservice: 
ms.assetid: 

# optional metadata

#audience:

ms.reviewer: traceyadams
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18, references_regions
ms.collection: M365-identity-device-management
---

# In development for Windows 365 Enterprise

To help in your readiness and planning, this page lists Windows 365 updates and features that are in development but not yet released. In addition to the information on this page:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for more updates.
- Similar features may be announced at different times for Windows 365 Business.

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
<!--## App management-->

<!--***********************************************-->
## Device management

### Admins can restore a Cloud PC to a previous state for a user<!--40784300-->
Windows 365 Business admins will be able to restore a Cloud PC to a previous state on behalf of the user. For more information about restoring Cloud PCs, see [restore-overview.md].

### New setting to easily enroll Business Cloud PCs in Microsoft Endpoint Manager<!--40009143-->

Admins will be able to set a toggle that automatically enrolls new Cloud PCs in to Microsoft Endpoint Manager.

### Resize action support for more Cloud PCs<!--40263425-->

The resize action will support Cloud PCs that are Azure Active Directory joined.

<!-- ***********************************************-->
<!--## Device provisioning-->

<!--***********************************************-->
<!--
## End user experience
-->

<!-- ***********************************************-->
## Monitor and troubleshoot

### System alerts and email notifications (preview)<!--40932899-->
You'll be able to set up system alerts and automated emails to be notified when certain events, warnings, or errors occur in the Windows 365 service. A subset of critical Cloud PC issues will be sent automatically to admins. In addition, you’ll be able to define alert rules, such as target audience (devices, user groups, tenants), thresholds, frequency, and notification channels.

### Cloud PC utilization report<!--40636545-->
A new report will be available for Cloud PCs. The **Cloud PC utilization** report will show how many hours users have been connected to their Cloud PCs. Information for individual Cloud PCs and aggregated data will be shown.

### Cloud PC wit connection quality issues report<!--40636545-->
A new report will be available for Cloud PCs. The **Cloud PCs with connection quality issues** report will show information for round-trip time, available bandwidth, and remoting sign-in time. Information for individual Cloud PCs and aggregated data will be shown.

### Review Cloud PC connectivity health checks and errors in Microsoft Endpoint Manager admin center<!--38469622 -->

You’ll be able to review connectivity health checks and errors in the Microsoft Endpoint Manager admin center to help you understand if your users are experiencing connectivity issues. You’ll also get a troubleshooting tool to help resolve connectivity issues.

### End user manual connectivity check<!--37679345 -->

End users will be able to manually run connectivity checks on their Cloud PCs from [windows365.microsoft.com](https://windows365.microsoft.com).

### Device history report – new information for Cloud PC performance<!--38310774  -->

The device history report will have new information to help you evaluate Cloud PC performance:

- Top five processes impacting CPU spike times
- Top five processes impacting RAM spike times

<!-- ***********************************************-->
<!-- ## Provisioning -->

<!-- ***********************************************-->
<!--## Role-based access control-->

## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
