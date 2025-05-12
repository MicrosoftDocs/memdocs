---
title: Complete migration
titleSuffix: Configuration Manager
description: Learn how to finish migration to a Configuration Manager current branch destination hierarchy after a source hierarchy no longer has data.
ms.date: 01/12/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: upgrade-and-migration-article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Plan to complete migration in Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager, you can complete the process of migration when a source hierarchy no longer has data that you want to migrate to your destination hierarchy. Completing migration includes the following general steps:  

-   Ensure that data you require has migrated. Before you complete migration from a source hierarchy, make sure that you have successfully migrated all of the resources from the source hierarchy that you require in the destination hierarchy. This can include data and clients.  

-   Stop gathering data from source sites. To complete migration from a source hierarchy, you must first stop gathering data from source sites.  

-   Clean up migration data. After you stop gathering data from all source sites in a source hierarchy, you can remove data about the migration process and source hierarchy from the database of the destination hierarchy.  

-   Decommission the source hierarchy. After you complete migration from a source hierarchy and that hierarchy no longer has resources that you manage, you can decommission the sites in the source hierarchy and remove the related infrastructure from your environment. For information about how to decommission sites and source hierarchies, consult the documentation for that version of Configuration Manager.  

Use the following sections to help you plan to complete migration from a source hierarchy by stopping data gathering and cleaning up migration data:  

-   [Plan to stop gathering data](#Plan_to_Stop_Data_Gath)  

-   [Plan to clean up migration data](#Plan_to_clean_up)  

##  <a name="Plan_to_Stop_Data_Gath"></a> Plan to stop gathering data  
 Before you complete migration and clean up migration data, you must stop gathering data from each source site in the source hierarchy. To stop gathering data from each source site, you must perform the **Stop Gathering Data** command on the bottom tier source sites, and then repeat the process at each parent site. The top-level site of the source hierarchy must be the last site on which you stop gathering data. You must stop data gathering at each child site before performing this command on a parent site. Typically, you only stop gathering data when you are ready to finish the migration process.  

 After you stop gathering data from a source site, shared distribution points from that site are no longer available as content locations for clients in the destination hierarchy. Therefore, ensure that any migrated content that the clients in the destination hierarchy require access to remains available by using one of the following options:  

-   In the destination hierarchy, distribute the content to at least one distribution point.  

-   Before you stop gathering data from a source site, upgrade or reassign shared distribution points that have the required content. For more about upgrading or reassigning shared distribution points, see the applicable sections in [Planning a content deployment migration strategy](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

After you stop gathering data from each source site in the source hierarchy, you can clean up migration data. Until you clean up migration data, each migration job that has run or that is scheduled to run remains accessible in the Configuration Manager console.  

For more about source sites and data gathering, see [Planning a source hierarchy strategy](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="Plan_to_clean_up"></a> Plan to clean up migration data  
 The last step required to finish migration is to clean up migration data. You can use the **Clean Up Migration Data** command after you have stopped gathering data for each source site in the source hierarchy. This optional action removes data about the current source hierarchy from the database of the destination hierarchy.  

 When you clean up migration data, most data about the migration is removed from the database of the destination hierarchy. However, details about migrated objects are retained. With these details, you can use the **Migration** workspace to reconfigure the source hierarchy that has the data that was migrated to resume migration from that source hierarchy, or to review the objects and site ownership of the objects that previously migrated.  
