---
# required metadata

title: In development - Windows 365 Enterprise
description: Windows 365 Enterprise features in development
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/12/2024
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
<!--## Device management-->

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

### Remoting connections report deprecation<!--52990648-->

The remoting connection report will be retired on December 31st, 2024. After this date, refer to the [Cloud PC connection quality report](report-cloud-pc-connection-quality.md).

<!-- ***********************************************-->
## Provisioning

### Windows 365 support for Spain Central region<!--54919607-->

Windows 365 Enterprise will support the Spain Central region. For more information, see [Supported Azure regions for Cloud PC provisioning](requirements.md?tabs=enterprise%2Cent#supported-azure-regions-for-cloud-pc-provisioning).

### Windows 365 support for Mexico Central region<!--54919656-->

Windows 365 Enterprise will support the Mexico Central region. For more information, see [Supported Azure regions for Cloud PC provisioning](requirements.md?tabs=enterprise%2Cent#supported-azure-regions-for-cloud-pc-provisioning).

<!-- ***********************************************-->
<!--## Security-->

<!-- ***********************************************
## Windows 365 app-->

<!-- ***********************************************-->
## Windows 365 Frontline

### Concurrency buffer usage alert<!--54902162-->

You’ll be able to set up a new alert to monitor concurrency buffer usage for Windows 365 Frontline in dedicated mode.

### More precise Windows 365 Frontline concurrency control<!--49324723-->

In a future update, you'll be able to allocate concurrent sessions for Windows 365 Frontline Cloud PCs in dedicated mode for each Microsoft Entra group assigned in the provisioning policy. This lets you reserve sessions to specific groups so sessions won't be consumed by other groups, and help you control your maximum concurrency limits.

## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
