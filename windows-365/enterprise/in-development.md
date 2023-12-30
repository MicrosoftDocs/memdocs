---
# required metadata

title: In development - Windows 365 Enterprise
titleSuffix: 
description: Windows 365 Enterprise features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 11/17/2023
ms.topic: conceptual
ms.service: windows-365
ms.subservice: 
ms.assetid: 

# optional metadata

#audience:

ms.reviewer: traceyadams
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18, references_regions
ms.collection:
- M365-identity-device-management
- tier2
---

# In development for Windows 365 Enterprise

To help in your readiness and planning, this page lists Windows 365 updates and features that are in development but not yet released. In addition to the information on this page:

- If we anticipate that you need to take action before a change, we'll publish a complementary post in Office message center.
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

<!-- ***********************************************-->
<!--## Device provisioning-->

<!--***********************************************-->
## End user experience

### Self-help in Windows 365 Business<!--45828334-->

A new self-help button for end users will be available in a future release of Windows 365 Business. End users will be able to click the **?** button and ask questions to find relevant help topics.

<!-- ***********************************************-->
<!--## Miscellaneous-->

<!-- ***********************************************-->
## Monitor and troubleshoot

### End user manual connectivity check<!--37679345 -->

End users will be able to manually run connectivity checks on their Cloud PCs from [windows365.microsoft.com](https://windows365.microsoft.com).

### New report: Cloud PCs that can't connect<!--45946128-->

A new report will be available that provides metrics that help admins evaluate tenant level device connection status and reliability.  For example, you'll be able to observe:
devices that have unhealthy hosts users' connections that consistently or frequently fail systemic issues, like an Azure infrastructure issue, that is impacting the ability of a user to connect.

### New alert rule: Cloud PCs that aren't available<!--47321010-->

A new alert rule will be available to notify you when Cloud PCs aren't available (not immediately available for Windows 365 Frontline). For more information about alerts in general, see [Alerts in Windows 365](alerts.md).

<!-- ***********************************************-->
## Provisioning

### New health check: UDP TURN (preview)<!--44505391-->

A new UDP TURN check will be added to the Azure Network Connections health checks. For more information about health checks, see [Azure network connections health checks](health-checks.md).

<!-- ***********************************************-->
## Security

### FQDN requirement changes<!--46731885-->

In a future update, Windows 365 will remove a large number of FQDNs from the current published list and move them to the existing *.infra.windows365.microsoft.com wildcard FQDN. This change will reduce the initial configuration requirements and the change rate of connectivity requirements. For Windows 365 Government, the FQDNs will be moved to *.infra.windows365.microsoft.us.

### Watermarking for Cloud PCs<!--45779621-->

You'll be able to turn on watermarking for Windows 365 Cloud PCs. Watermarking, alongside screen capture protection, helps prevent sensitive information from being captured on client endpoints. When you enable watermarking, QR code watermarks appear on the Cloud PC desktop. The QR code contains the connection ID of a remote session that admins can use to trace the session.


<!-- ***********************************************
## Windows 365 app-->


## Next steps

For details about recent developments, see [What's new in Windows 365](whats-new.md).
