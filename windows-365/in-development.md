---
# required metadata

title: In development - Windows 365
titleSuffix: 
description: Windows 365 features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 8/11/2021
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
## Device management

### End grace period option<!-- 34841603-->

Currently, certain conditions will put a Cloud PC into a seven-day grace period. At the end of this time the Cloud PC will be deprovisioned and user will lose access.

In a future update, you’ll be able to immediately end the grace period for individual Cloud PCs. By ending the grace period manually, you won’t have to wait the full seven days to remove user access from the Cloud PC.

For more information on grace periods, see [Device management overview for Cloud PCs](device-management-overview.md).

### Support for Azure AD joined Cloud PCs<!-- 35060203-->

Windows 365 Enterprise will support Cloud PCs that are Azure AD Joined. These devices will run in a Microsoft-hosted network, so customers:

- Don’t need their own Azure infrastructure
- Don’t need to create an on-premises network connection.

### Support for Windows 11<!--35091970 -->

In a future update, Windows 365 will support Windows 11 as a Cloud PC operating system.

### Support for Cloud PC sizes based on virtual graphics processing units (GPU)<!--35091874 -->

New Windows 365 licenses will be available that include virtual graphics processing unit options that support advanced graphic workloads on Cloud PCs.

<!-- ***********************************************-->
## Monitor and troubleshoot

### Resource performance report in Endpoint Analytics<!-- 32978343-->

A new report will be added to Endpoint Analytics: the **Resource performance report**. This report will include metrics for CPU and RAM performance on Cloud PCs.

### Remoting connection report in Endpoint Analytics<!-- 33039368-->

A new repot will be added to Endpoint Analytics: the **Remoting connection report**. This report will include the following metrics:

- **Cloud PC Sign in time (sec)** provides the total time users take to connect to the cloud PC.
- **Round Trip Time (ms)** provides insights on the speed and reliability of network connections from the user location.

## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
