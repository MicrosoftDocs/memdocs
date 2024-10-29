---
title: Migrate data
titleSuffix: Configuration Manager
description: Learn how to transfer data from a source hierarchy to a Configuration Manager destination hierarchy.
ms.date: 11/05/2018
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Migrate data between hierarchies in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use migration to transfer data from a supported source hierarchy to your Configuration Manager (current branch) destination hierarchy. When you migrate data from a source hierarchy:  

- You access data from the site databases in the source infrastructure, and then transfer that data to your current environment.  

- Migration doesn't change the data in the source hierarchy. Instead it discovers the data and stores a copy in the database of the destination hierarchy.  

Consider the following points when you plan your migration strategy:  

- You can migrate an existing Configuration Manager 2007 SP2 infrastructure to Configuration Manager (current branch).  

- You can migrate some or all of the supported data from a source site.  

- You can migrate the data from a single source site to several different sites in the destination hierarchy.  

- You can move data from multiple source sites to a single site in the destination hierarchy.  


The following video discusses and demonstrates two common [migration scenarios](#BKMK_MigrationScenarios). It also includes options for including Microsoft Azure in migration plans.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="BKMK_MigrationConcepts"></a> Concepts  

 Configuration Manager uses the following concepts and terms during migration.  

#### Source hierarchy
A hierarchy that runs a supported version of Configuration Manager and has data that you want to migrate. When you set up migration, you identify the source hierarchy when you specify the top-level site of a source hierarchy. After you specify a source hierarchy, the top-level site of the destination hierarchy gathers data from the database of the designated source site to identify the data that you can migrate. 

For more information, see [Source hierarchies](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### Source sites
The sites in the source hierarchy that have data that you can migrate to your destination hierarchy. 

For more information, see [Source sites](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### Destination hierarchy
A Configuration Manager (current branch) hierarchy where migration runs to import data from a source hierarchy.

#### Data gathering
The ongoing process of identifying the information in a source hierarchy that you can migrate to your destination hierarchy. Configuration Manager checks the source hierarchy on a schedule. This process identifies any changes to information in the source hierarchy that you previously migrated and that you might want to update in the destination hierarchy.

For more information, see [Data gathering](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### Migration jobs
The process of configuring the specific objects to migrate, and then managing the migration of those objects to the destination hierarchy.

For more information, see [Planning a migration job strategy](planning-a-migration-job-strategy.md).

#### Client migration
The process of transferring information that clients use from the database of the source site to the database of the destination hierarchy. This migration of data is then followed by an upgrade of client software on devices to the client software version from the destination hierarchy.

For more information, see [Planning a client migration strategy](planning-a-client-migration-strategy.md).

#### Shared distribution points
The distribution points from the source hierarchy that Configuration Manager shares with the destination hierarchy during the migration period.

During the migration period, clients assigned to sites in the destination hierarchy can get content from shared distribution points.

For more information, see [Share distribution points between source and destination hierarchies](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration).

#### Monitoring migration
The process of monitoring migration activities. You monitor migration progress and success from the **Migration** node in the **Administration** workspace.

For more information, see [Planning to monitor migration activity](planning-to-monitor-migration-activity.md).

#### Stop gathering data
The process of stopping data gathering from source sites. When you no longer have data to migrate from a source hierarchy, or if you want to pause migration-related activities, you can configure the destination hierarchy to stop gathering data from the source hierarchy.

For more information, see [Data gathering](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### Clean up migration data
The process of finishing migration from a source hierarchy by removing information about the migration from the destination hierarchies database.

For more information, see [Planning to complete migration](planning-to-complete-migration.md).



## Typical workflow  

To set up a workflow for migration:

1.  Specify a supported source hierarchy.  

2.  Set up data gathering. Data gathering enables Configuration Manager to collect information about data that can migrate from the source hierarchy.  

     Configuration Manager automatically repeats the process to collect data on a simple schedule until you stop the data gathering process. By default, the data gathering process repeats every four hours so that Configuration Manager can identify changes to data in the source hierarchy. Data gathering is also necessary to share distribution points.  

3.  Create migration jobs to migrate data between the source and destination hierarchy.  

4.  You can stop the data gathering process at any time by using the **Stop Gathering Data** action. When you stop data gathering, Configuration Manager no longer identifies changes to data in the source hierarchy and can no longer share distribution points. Typically, you use this action when you no longer plan to migrate data or share distribution points from the source hierarchy.  

5.  Optionally, after data gathering has stopped at all sites for the source hierarchy, you can clean up the migration data by using the **Clean Up Migration Data** action. This action deletes the historical data about migration from a source hierarchy from the database of the destination hierarchy.  

After you migrate data, and you no longer need the source hierarchy to manage devices in your environment, you can decommission that source hierarchy and infrastructure.  



##  <a name="BKMK_MigrationScenarios"></a> Scenarios  

 Configuration Manager supports the following migration scenarios:
- [Migration from Configuration Manager 2007 hierarchies](#bkmk_2007)  
- [Migration from Configuration Manager 2012 or another Configuration Manager hierarchy](#bkmk_2012)

> [!NOTE]  
>  The expansion of a hierarchy that has a standalone site into a hierarchy that has a central administration site isn't categorized as a migration. For information about hierarchy expansion, see [Expand a stand-alone primary site](../servers/deploy/install/setup-wizard-central-primary.md#expand-a-stand-alone-primary-site).  


### <a name="bkmk_2007"></a> Migration from Configuration Manager 2007 hierarchies  

 When you use migration to migrate data from Configuration Manager 2007, you can maintain your investment in your existing site infrastructure and gain the following benefits:  

#### Site database improvements
The Configuration Manager (current branch) database supports full Unicode.

#### Database replication between sites
Replication in Configuration Manager (current branch) is based on Microsoft SQL Server. This behavior improves the performance of site-to-site data transfer.

#### User-centric management
Users are the focus of management tasks in Configuration Manager (current branch). For example, you can distribute software to a user even if you don't know the device name for that user. Additionally, Configuration Manager gives users much more control over what software is installed on their devices and when that software is installed.

#### Hierarchy simplification
Configuration Manager (current branch) lets you build a simpler site hierarchy. This improvement is due to the introduction of the central administration site type and changes to the behavior of primary and secondary sites. Configuration Manager (current branch) uses less network bandwidth and requires fewer servers than previous versions.

#### Role-based administration
This central security model in Configuration Manager (current branch) offers hierarchy-wide security and management that corresponds to your administrative and business requirements.

> [!NOTE]  
>  Because of design changes that were first introduced in System Center 2012 Configuration Manager, you can't upgrade Configuration Manager 2007 to Configuration Manager (current branch). In-place upgrade is supported from System Center 2012 Configuration Manager to Configuration Manager (current branch).  


### <a name="bkmk_2012"></a> Migration from Configuration Manager 2012 or another Configuration Manager hierarchy  
 The process of migrating data from a System Center 2012 Configuration Manager or Configuration Manager hierarchy is the same. This process includes migrating data from multiple source hierarchies into a single destination hierarchy. You might use this process when your company gets additional resources that are already managed by Configuration Manager. Additionally, you can migrate data from a test environment to your Configuration Manager production environment. This process lets you maintain your investment in the Configuration Manager test environment.  



## See also  

-   [Planning for migration to Configuration Manager](planning-for-migration.md)  

-   [Configuring source hierarchies and source sites for migration](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operations for migration](operations-for-migration.md)  

-   [Security and privacy for migration](security-and-privacy-for-migration.md)  

-   [Start using Configuration Manager](../servers/deploy/start-using.md)
