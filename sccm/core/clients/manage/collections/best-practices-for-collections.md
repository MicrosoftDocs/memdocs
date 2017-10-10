---
title: "Collections best practices"
description: "Get best practices for collections in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: 4
caps.handback.revision: 0
author: andredm7 
ms.author: andredm
manager: angrobe

---
# Best practices for collections in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the following best practices for collections in System Center Configuration Manager.  

## Do not use incremental updates for a large number of collections  
 When you enable the **Use incremental updates for this collection** option, this configuration might cause evaluation delays when you enable it for many collections. The threshold is about 200 collections in your hierarchy. The exact number depends on the following factors:  

-   The total number of collections  

-   The frequency of new resources being added and changed in the hierarchy  

-   The number of clients in your hierarchy  

-   The complexity of collection membership rules in your hierarchy  

## Make sure that maintenance windows are large enough to deploy critical software updates  
 You can configure maintenance windows for device collections to restrict the times that Configuration Manager can install software on these devices. If you configure the maintenance window to be too small, the client might not be able to install critical software updates, which leaves the client vulnerable to the attack that is mitigated by the software update.  
