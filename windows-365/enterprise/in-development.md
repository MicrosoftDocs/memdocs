---
# required metadata

title: In development - Windows 365 Enterprise
titleSuffix: 
description: Windows 365 Enterprise features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 02/16/2022
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

-->

<!-- ***********************************************-->
## App management

### Use conditional access to group Windows 365 and Azure Virtual Desktop app policies together <!-- 36360788 -->

In a future update, you’ll be able to target Conditional Access (CA) policies to a single application that applies to both the Windows 365 and Azure Virtual Desktop apps.

Currently, Windows 365 and Azure Virtual Desktop share a common framework for identity access by using Azure Active Directory (Azure AD) and security controls with CA policies. You can target CA policies to the Windows 365 app and this applies only to windows365.microsoft.com web client. To apply CA policies to the full Windows client and non-windows clients, you must assign CA policies to both the Windows 365 and Azure Virtual Desktop apps.  For more information, see [Assign a Conditional Access policy for Cloud PCs](set-conditional-access-policies.md).

<!-- ***********************************************-->
## Device management

### Nested virtualizations<!--37800910-->

In a future release, Windows 365 8vCPU/32GB licenses will support nested virtualizations most currently supported regions. Southeast Asia and West US 2 will follow at a later date.

### Operating system end of support status for Cloud PCs<!--36852572 -->

The **Provisioning policies** page is getting a new column: **Image status**. It tells you if the device image for each provisioning policy uses an operating system (OS) that is supported by Microsoft Windows security and other updates.

### Point-in-time restore<!--37063579 -->

Administrators and users will be able to restore a Cloud PC to a state from a previous point in time. Multiple near-term and long-term restore points will be available. Administrators will be able to:

- Configure the restore point frequency
- Grant or deny users restore permissions
- Bulk restore

<!-- ***********************************************-->
## Monitor and troubleshoot

### End user manual connectivity check<!--37679345 -->

End users will be able to manually run connectivity checks on their Cloud PCs from [windows365.microsoft.com](https://windows365.microsoft.com).

<!-- ***********************************************-->
<!-- ## Provisioning -->


<!-- ***********************************************-->
<!--## Role-based access control-->

## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
