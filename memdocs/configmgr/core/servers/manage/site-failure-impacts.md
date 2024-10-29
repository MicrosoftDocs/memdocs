---
title: Site failure impacts
titleSuffix: Configuration Manager
description: Understand the effects of various failures in a Configuration Manager site.
ms.date: 07/30/2018
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Site failure impacts in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The site server and any of the other site systems can fail and cause a loss of the services they regularly provide. If you install multiple site systems on the same computer, and that computer fails, all services regularly provided by those site systems are no longer available.

Part of your planning process should include understanding the impact on the service that you provide your organization. Because each site system in the site provides different functionality, the impact of a failure on the site differs, depending on the role of the site system that failed. 

Use [high availability options](../deploy/configure/high-availability-options.md) to help mitigate the failure of any single system. Also plan for and practice a [backup and recovery](backup-and-recovery.md) strategy to reduce the amount of time the service is unavailable.

The following sections describe the impact when the specified site system isn't operational:


### Site server

- No site administration is possible. You can't connect the console to the site.  

- The management point collects client information and caches it until the site server is back online.  

- Users can run existing deployments, and clients can download content from distribution points.  


### Site database

- No site administration is possible.  

- If the Configuration Manager client already has a policy assignment with new policies, and if the management point has cached the policy body, the client can make a policy body request and receive the policy body reply. However, the site can't service any new policy assignment requests.  

- Clients can run deployments, only if they've already received the policy, and the associated source files are already cached locally at the client.  


### Management point

- Although you can create new deployments, clients don't receive them until a management point is online.  

- Clients still collect inventory, software metering, and status information. They store this data locally until the management point is available.  

- Clients can run deployments, only if they've already received the policy, and the associated source files are already cached locally at the client.  


### Distribution point

- Configuration Manager clients can run deployments, only if the associated source files have already been downloaded locally or are available on a peer source.

