---
title: Site failure impacts
titleSuffix: Configuration Manager
description: Understand the effects of various failures in a Configuration Manager site.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Site failure impacts in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The site server and any of the other site systems can fail and cause a loss of the services they regularly provide. If you install multiple site systems on the same computer, and that computer fails, all services regularly provided by those site systems are no longer available.

Part of your planning process should include understanding the impact on the service that you provide your organization. Because each site system in the site provides different functionality, the impact of a failure on the site differs, depending on the role of the site system that failed. 

Use [high availability options](/sccm/core/servers/deploy/configure/high-availability-options) to help mitigate the failure of any single system. Also plan for and practice a [backup and recovery](/sccm/core/servers/manage/backup-and-recovery) strategy to reduce the amount of time the service is unavailable.

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

