---
title: "Synchronize the Software Update Point"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: b394b01f-a87b-4f15-b364-558184921871searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Synchronizing the Software Update Point
In System Center Configuration Manager, software updates must be synchronized before the update information is available in the System Center Configuration Manager console. Synchronization is initiated at the highest level site in the hierarchy that has a software update point.  

> [!NOTE]
>  General information about Software Updates can be found in the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt346023.aspx) under [Deploy and manage software updates in System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt634340.aspx).  

## Software Updates Synchronization  
 Software updates synchronization in Configuration Manager is the process of retrieving the software updates metadata that meet the configured criteria from the upstream Windows Server Update Services (WSUS) server or from Microsoft Update. The highest site in the Configuration Manager hierarchy with a software update point (most likely the central site) synchronizes with Microsoft Update. This synchronization can be scheduled as part of the software update point properties, or it can be manually initiated.  

 There are two types of synchronization:  

-   A full synchronization, which synchronizes the whole catalog of updates on the WSUS server. At the end of the full synchronization, the Configuration Manager database will match the content of WSUS filtered by the current subscription.  

-   A delta synchronization, which synchronizes only changes (adds and removals) that occurred since the last successful synchronization. A delta synchronization will not examine at updates synchronized earlier and not changed since.  

> [!IMPORTANT]
>  While they are nearly identical functionally, a full synchronization will potentially repair updates from previous synchronizations that have gotten damaged or deleted. A delta synchronization will not repair any updates from previous synchronizations.  

 In System Center Configuration ManagerSP1 most synchronizations, both manual and scheduled, perform a delta synchronization. A synchronization will escalate to a full synchronization if there are configuration changes that require a full synchronization, such as: switching to a different default SUP, changes in the subscription, changes in the supersedence mode or window. A synchronization will also escalate to a full synchronization periodically every 7 days (a period configurable in the site control file under "Full Sync Interval (days)").  

## See Also  
 [Configuration Manager SDK](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Software Updates](../../develop/sum/software-updates.md)   
 [Other Deployment Options](../../develop/sum/synchronizing-the-software-update-point.md)
