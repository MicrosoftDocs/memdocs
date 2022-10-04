---
title: Plan for migration
titleSuffix: Configuration Manager
description: Learn about sites and hierarchies before you migrate data to a Configuration Manager current branch destination hierarchy.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Plan for migration to Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Before you migrate data to a Configuration Manager current branch destination hierarchy, make sure that you are familiar with sites and hierarchies in Configuration Manager. For more about sites and hierarchies, see [Fundamentals of Configuration Manager](../../core/understand/fundamentals.md).  

Install a Configuration Manager current branch hierarchy to be the destination hierarchy before you migrate data from a supported source hierarchy.  

After you install the destination hierarchy, set up the management features and functions that you want to use in your destination hierarchy before you start to migrate data.  

Additionally, you might have to plan for overlap between the source hierarchy and your destination hierarchy. For example, you might set up the source hierarchy to use the same network locations or boundaries as your destination hierarchy, and you then install new clients to your destination hierarchy and use automatic site assignment. In this scenario, because a newly installed Configuration Manager client can select a site to join from either hierarchy, the client might incorrectly assign to your source hierarchy. Therefore, plan to assign each new client in the destination hierarchy to a specific site in that hierarchy instead of using automatic site assignment.  

For more about site assignments, see [Client site assignment considerations](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#client-site-assignment-considerations) in [Interoperability between different versions of Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

Use the following articles to help you plan how to migrate a supported source hierarchy to a Configuration Manager destination hierarchy:

-   [Prerequisites for migration](../../core/migration/prerequisites-for-migration.md)  

-   [Administrator checklists for migration planning](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determine whether to migrate data to Configuration Manager current branch](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Plan a source hierarchy strategy](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Administrator checklists for migration planning](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Plan a client migration strategy](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Plan a content deployment migration strategy](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Plan for the migration of Configuration Manager objects to Configuration Manager current branch](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Plan to monitor migration activity](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Plan to complete migration](../../core/migration/planning-to-complete-migration.md)  
