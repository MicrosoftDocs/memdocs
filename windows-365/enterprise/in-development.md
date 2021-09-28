---
# required metadata

title: In development - Windows 365
titleSuffix: 
description: Windows 365 features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 9/28/2021
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# In development for Windows 365 Enterprise

To help in your readiness and planning, this page lists Windows 365 updates and features that are in development but not yet released. In addition to the information on this page:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for more updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Windows 365 capabilities in an upcoming release. Dates and individual features might change. This page doesn't describe all features in development.

**This article was last updated on the date listed under the title above.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->

<!-- ***********************************************-->
## App management

### Use conditional access to group Windows 365 and Azure Virtual Desktop app policies together <!-- 36360788 -->

In a future update, you’ll be able to target CA policies to a single application that applies to both the Windows 365 and Azure Virtual Desktop apps.

Currently, Windows 365 and Azure Virtual Desktop share a common framework for identity access by using Azure Active Directory (Azure AD) and security controls with Conditional Access (CA) policies. You can target CA policies to the Windows 365 app and this applies only to windows365.microsoft.com web client. To apply CA policies to the full Windows client and non-windows clients, you must assign CA policies to both the Windows 365 and Azure Virtual Desktop apps.  For more information, see [Assign a Conditional Access policy for Cloud PCs](set-conditional-access-policies.md).

<!-- ***********************************************-->
## Device management

### Support for Azure AD joined Cloud PCs<!-- 35060203-->

Windows 365 Enterprise will support Cloud PCs that are Azure AD Joined. These devices will run in a Microsoft-hosted network, so customers:

- Don’t need their own Azure infrastructure
- Don’t need to create an on-premises network connection.

### Support for Windows 11<!--35091970 -->

In a future update, Windows 365 will support Windows 11 as a Cloud PC operating system.

Windows 11 Cloud PCs require Generation 2 (Gen2) virtual machines. For information about converting existing Generation 1 custom device images to Gen2, see [Convert an existing custom device image to a generation 2 virtual machine](device-images-convert-generation-2.md).

### Support for Cloud PC sizes based on virtual graphics processing units (GPU)<!--35091874 -->

New Windows 365 licenses will be available that include virtual graphics processing unit options that support advanced graphic workloads on Cloud PCs.

<!-- ***********************************************-->
## Role-based access control

### Windows 365 Administrator role<!--5827123-->

In a future update, the Windows 365 Administrator role will be available for admins by using role assignment in the Microsoft Admin Center and Azure Active Directory (AAD). With this role, admins can broadly manage Windows 365 Enterprise Cloud PCs, users, devices, and groups. This new role is in addition to the other existing roles that Windows 365 currently supports: Azure AD Global Admin, Intune Admin, and Cloud PC granular roles in Microsoft Endpoint Manager.

## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
