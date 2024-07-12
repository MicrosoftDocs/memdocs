---
# required metadata
title: Windows 365 service architecture and resilience
titleSuffix:
description: Learn about Windows 365 service resilience.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 07/16/2024
ms.topic: conceptual
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: thhickli
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- M365-identity-device-management
- tier2
---

# Windows 365 service resilience

Windows 365 is designed to provide a resilient and reliable service for organizations and end users. Windows 365 uses [Azure Virtual Desktop services]((/azure/virtual-desktop/service-architecture-resilience)) to let end users connect to their Cloud PC in any of the supported Azure regions from anywhere, on any device. To withstand outages and support end user and administrator requests at all times, resilience is architected into these services.

Windows 365 is a software as a service (SaaS) service, where customers of the service do not have to architect, deploy, or manage complex infrastructure. As a SaaS service, Microsoft manages the underlying infrastructure for all of the individual Windows 365 services to maintain a global, fully available, resilient service that customers can rely upon for the daily use of their Cloud PCs. Microsoft continually works to improve the architecture of the service to improve the resilience and recovery times should there be an outage in any of the related Azure services.

In addition to the Azure Virtual Desktop connectivity layer, Windows 365 operates many dedicated services that are architected as microservices to support agile operations and independence. Each of these performs specific tasks related to administrator or end user requests. Some examples include:

- The Windows 365 provisioning service processes deployment requests to provision Cloud PCs according to the specifications and locations defined by teh administrator making hte request.
- The Entra ID notification service monitors administrator changes to Microsoft Entra ID groups that trigger new deployments.
- Other services manage
  - The administrator portal
  - The end user portal
  - Disaster recovery
  - Diagnostics
  - Troubleshooting
  - Service monitoring
  - And all other functions of Windows 365.  

Each of these services:

- Use standard Azure services
- Is architected to use Azure resilience services like Azure availability zones.
- Is its own web service that has a certain set of additional Azure infrastructure requirements like CosmosBD, Azure storage, and Event hubs.

The following diagram shows the architecture of an example service. Windows 365 distributes its infrastructure across multiple availability zones within a region as well as across multiple Azure regions. This supports in-region and cross-region resiliency. If an outage occurs within a region, the service continues functioning. If a region fails, the service is transferred to the secondary region's infrastructure, and normal operations continue.

<!-- ########################## -->
## Next steps

[Windows 365 architecture](architecture.md)]
[High-level architecture diagram for Windows 365](high-level-architecture.md)
