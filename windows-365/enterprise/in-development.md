---
# required metadata

title: In development - Windows 365 Enterprise
description: Windows 365 Enterprise features in development
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/26/2024
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

In a future update, RDP Shortpath in Windows 365 will support establishing an indirect UDP connection using Traversal Using Relays around NAT (TURN) for symmetric NAT.  TURN is a popular standard for device-to-device networking for low latency, high-throughput data transmission. For more information, see [Network Traversal Concepts](/azure/communication-services/concepts/network-traversal). For more information about RDP Shortpath, see [Use RDP Shortpath for public networks with Windows 365](rdp-shortpath-public-networks.md).

### Chroma subsampling default change to 4:2:0<!--50308895-->

To reduce monitor support issues, the Windows 365 service will default the chroma subsampling at 4:2:0 (instead of the previous 4:4:4).

<!-- ***********************************************-->
## Device security

### Windows 365 Government support for Customer Lockbox<!--48802385-->

Windows 365 Government will support Microsoft Purview Customer Lockbox.

For more information, see [Microsoft Purview Customer Lockbox](/purview/customer-lockbox-requests).

### Closing port 3389 by default for newly provisioned Cloud PCs<!--51154043-->

To help secure your Windows 365 environment, the inbound port 3389 will be closed by default.

### Cloud PC support for FIDO devices and passkeys on macOS and iOS<!--51858977-->

Windows 365 Cloud PCs will support FIDO devices and passkeys for Microsoft Entra ID sign in on macOS and iOS.

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

<!-- ***********************************************-->
## Provisioning

### New health check: UDP TURN (preview)<!--44505391-->

A new UDP TURN check will be added to the Azure Network Connections health checks. For more information about health checks, see [Azure network connections health checks](health-checks.md).

<!-- ***********************************************-->
## Security

### New settings for Windows 365 security baselines<!--49685126-->

New configuration settings will be introduced for the Windows 365 security baseline.

<!-- ***********************************************
## Windows 365 app-->

<!-- ***********************************************-->
<!--## Windows 365 Frontline-->


## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
