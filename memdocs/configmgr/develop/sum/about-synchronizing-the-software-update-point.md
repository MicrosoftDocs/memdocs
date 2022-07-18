---
title: "Synchronize the Software Update Point"
description: In Configuration Manager, software updates must be synchronized before the update information is available in the Configuration Manager console.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b394b01f-a87b-4f15-b364-558184921871
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Synchronizing the Software Update Point
In Configuration Manager, software updates must be synchronized before the update information is available in the Configuration Manager console. Synchronization is initiated at the highest level site in the hierarchy that has a software update point.  

For more information about software updates, see [Deploy and manage software updates](../../sum/understand/software-updates-introduction.md).  

## Software Updates Synchronization  
 Software updates synchronization in Configuration Manager is the process of retrieving the software updates metadata that meet the configured criteria from the upstream Windows Server Update Services (WSUS) server or from Microsoft Update. The highest site in the Configuration Manager hierarchy with a software update point (most likely the central site) synchronizes with Microsoft Update. This synchronization can be scheduled as part of the software update point properties, or it can be manually initiated.  

 There are two types of synchronization:  

-   A full synchronization, which synchronizes the whole catalog of updates on the WSUS server. At the end of the full synchronization, the Configuration Manager database will match the content of WSUS filtered by the current subscription.  

-   A delta synchronization, which synchronizes only changes (adds and removals) that occurred since the last successful synchronization. A delta synchronization will not examine any updates synchronized earlier and not changed since.  

> [!IMPORTANT]
>  While they are nearly identical functionally, a full synchronization will potentially repair updates from previous synchronizations that have gotten damaged or deleted. A delta synchronization will not repair any updates from previous synchronizations.  

 in Configuration ManagerSP1 most synchronizations, both manual and scheduled, perform a delta synchronization. A synchronization will escalate to a full synchronization if there are configuration changes that require a full synchronization, such as: switching to a different default SUP, changes in the subscription, changes in the supersedence mode or window. A synchronization will also escalate to a full synchronization periodically every 7 days (a period configurable in the site control file under "Full Sync Interval (days)").  
