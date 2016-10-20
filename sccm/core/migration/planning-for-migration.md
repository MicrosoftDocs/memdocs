---
title: "Plan for migration | System Center Configuration Manager"
description: "Learn about sites and hierarchies before you migrate data to a System Center Configuration Manager destination hierarchy."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Planning for migration to System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Before you migrate data to a System Center Configuration Manager destination hierarchy, make sure that you are familiar with sites and hierarchies in Configuration Manager. For more information about sites and hierarchies, see [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md).  

 You must first install a System Center Configuration Manager hierarchy to be the destination hierarchy before you can migrate data from a supported source hierarchy.  

 After you install the destination hierarchy, configure the management features and functions that you want to use in your destination hierarchy before you start to migrate data.  

 Additionally, you might have to plan for overlap between the source hierarchy and your destination hierarchy. As an example, consider when the source hierarchy is configured to use the same network locations or boundaries as your destination hierarchy and you then install new clients to your destination hierarchy and use automatic site assignment. In this scenario, because a newly installed Configuration Manager client can select a site to join from either hierarchy, the client could incorrectly assign to your source hierarchy. Therefore, plan to assign each new client in the destination hierarchy to a specific site in that hierarchy instead of using automatic-site assignment.  

 For more information about site assignments, see the [Client site assignment considerations](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) section in the [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md) topic.  

## Planning Topics  
 Use the following topics to help you plan how to migrate a supported source hierarchy to a System Center Configuration Manager destination hierarchy:  

-   [Prerequisites for migration in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Administrator checklists for migration planning in System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determine whether to migrate data to System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Administrator checklists for migration planning in System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planning for the migration of Configuration Manager objects to System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planning to monitor migration activity in System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  
