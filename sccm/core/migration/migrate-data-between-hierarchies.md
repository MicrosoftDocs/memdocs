---
title: "Migrate data"
titleSuffix: "Configuration Manager"
description: "Learn how to transfer data from a source hierarchy to a System Center Configuration Manager destination hierarchy."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: 11
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Migrate data between hierarchies in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use migration to transfer data from a supported source hierarchy to your System Center Configuration Manager destination hierarchy.  When you migrate data from a source hierarchy:  

-   You access data from the site databases that you identify in the source infrastructure and then transfer that data to your current environment.  

-   Migration does not change the data in the source hierarchy, but instead discovers the data and stores a copy in the database of the destination hierarchy.  

Consider the following when you plan your migration strategy:  

-   You can migrate an existing Configuration Manager 2007 SP2 infrastructure to System Center Configuration Manager.  

-   You can migrate some or all of the supported data from a source site.  

-   You can migrate the data from a single source site to several different sites in the destination hierarchy.  

-   You can move data from multiple source sites to a single site in the destination hierarchy.  

##  <a name="BKMK_MigrationConcepts"></a> Concepts for Migration  
 You might encounter the following concepts and terms when you use migration.  

|Concept or term|More information|  
|---------------------|----------------------|  
|Source hierarchy|A hierarchy that runs a supported version of Configuration Manager and has data that you want to migrate. When you set up migration, you identify the source hierarchy when you specify the top-level site of a source hierarchy. After you specify a source hierarchy, the top-level site of the destination hierarchy gathers data from the database of the designated source site to identify the data that you can migrate.<br /><br /> For more information, see [Source hierarchies](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies) in [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Source sites|The sites in the source hierarchy that have data that you can migrate to your destination hierarchy.<br /><br /> For more information, see [Source sites](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites) in [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Destination hierarchy|A System Center Configuration Manager hierarchy where migration runs to import data from a source hierarchy.|  
|Data gathering|The ongoing process of identifying the information in a source hierarchy that you can migrate to your destination hierarchy. Configuration Manager checks the source hierarchy on a schedule to identify any changes to information in the source hierarchy that you previously migrated and that you might want to update in the destination hierarchy.<br /><br /> For more information, see [Data gathering](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) in [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Migration jobs|The process of configuring the specific objects to migrate, and then managing the migration of those objects to the destination hierarchy.<br /><br /> For more information, see [Planning a migration job strategy in System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)|  
|Client migration|The process of transferring information that clients use from the database of the source site to the database of the destination hierarchy. This migration of data is then followed by an upgrade of client software on devices to the  client software version from the destination hierarchy.<br /><br /> For more information, see [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).|  
|Shared distribution points|The distribution points from the source hierarchy that are shared with the destination hierarchy during the migration period.<br /><br /> During the migration period, clients assigned to sites in the destination hierarchy can get content from shared distribution points.<br /><br /> For more information, see [Share distribution points between source and destination hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).|  
|Monitoring migration|The process of monitoring migration activities. You monitor migration progress and success from the **Migration** node in the **Administration** workspace.<br /><br /> For more information, see [Planning to monitor migration activity in System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md).|  
|Stop gathering data|The process of stopping data gathering from source sites. When you no longer have data to migrate from a source hierarchy, or if you want to pause migration-related activities, you can configure the destination hierarchy to stop gathering data from the source hierarchy.<br /><br /> For more information, see [Data gathering](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) in [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Clean up migration data|The process of finishing migration from a source hierarchy by removing information about the migration from the destination hierarchies database.<br /><br /> For more information, see [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).|  

## Typical workflow for migration  
To set up a workflow for migration:

1.  Specify a supported source hierarchy.  

2.  Set up data gathering. Data gathering enables Configuration Manager to collect information about data that can migrate from the source hierarchy.  

     Configuration Manager automatically repeats the process to collect data on a simple schedule until you stop the data gathering process. By default, the data gathering process repeats every four hours so that Configuration Manager can identify changes to data in the source hierarchy that you might want to migrate. Data gathering is also necessary to share distribution points from the source hierarchy to the destination hierarchy.  

3.  Create migration jobs to migrate data between the source and destination hierarchy.  

4.  You can stop the data gathering process at any time by using the **Stop Gathering Data** command. When you stop data gathering, Configuration Manager no longer identifies changes to data in the source hierarchy and can no longer share distribution points between the source and destination hierarchies. Typically, you use this action when you no longer plan to migrate data or share distribution points from the source hierarchy.  

5.  Optionally, after data gathering has stopped at all sites for the source hierarchy, you can clean up the migration data by using the **Clean Up Migration Data** command. This command deletes the historical data about migration from a source hierarchy from the database of the destination hierarchy.  

After you migrate data from a Configuration Manager source hierarchy that you will no longer use to manage your environment, you can decommission that source hierarchy and infrastructure.  

##  <a name="BKMK_MigrationScenarios"></a> Migration scenarios  
 Configuration Manager supports the following migration scenarios.  

> [!NOTE]  
>  The expansion of a hierarchy that has a standalone site into a hierarchy that has a central administration site is not categorized as a migration. For information about hierarchy expansion, see [Expand a stand-alone primary site](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) in [Use the Setup Wizard to install sites](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

### Migration from Configuration Manager 2007 hierarchies  
 When you use migration to migrate data from Configuration Manager 2007, you can maintain your investment in your existing site infrastructure and gain the following benefits:  

|Benefit|More information|  
|-------------|----------------------|  
|Site database improvements|The System Center Configuration Manager database supports full Unicode.|  
|Database replication between sites|Replication in System Center Configuration Manager is based on Microsoft SQL Server. This improves the performance of site-to-site data transfer.|  
|User-centric management|Users are the focus of management tasks in System Center Configuration Manager. For example, you can distribute software to a user even if you do not know the device name for that user. Additionally, System Center Configuration Manager gives users much more control over what software is installed on their devices and when that software is installed.|  
|Hierarchy simplification|In System Center Configuration Manager, the  central administration site type and changes to the behavior of primary and secondary sites let you build a simpler site hierarchy that uses less network bandwidth and requires fewer servers.|  
|Role-based administration|This central security model in System Center Configuration Manager offers hierarchy-wide security and management that corresponds to your administrative and business requirements.|  

> [!NOTE]  
>  Because of design changes that were first introduced in System Center 2012 Configuration Manager, you cannot upgrade Configuration Manager 2007 infrastructure to System Center Configuration Manager. In-place upgrade is supported from System Center 2012 Configuration Manager to System Center Configuration Manager.  

### Migration from Configuration Manager 2012 or another System Center Configuration Manager hierarchy  
 The process of migrating data from a System Center 2012 Configuration Manager or System Center Configuration Manager hierarchy is the same. This includes migrating data from multiple source hierarchies into a single destination hierarchy, like when your company gets additional resources that are already managed by Configuration Manager. Additionally, you can migrate data from a test environment to your Configuration Manager production environment. This lets you maintain your investment in the Configuration Manager test environment.  

## Additional topics for migration:  

-   [Planning for migration to System Center Configuration Manager](../../core/migration/planning-for-migration.md)  

-   [Configuring source hierarchies and source sites for migration to System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operations for migrating to System Center Configuration Manager](../../core/migration/operations-for-migration.md)  

-   [Security and privacy for migration to System Center Configuration Manager](../../core/migration/security-and-privacy-for-migration.md)  

## See Also  
 [Start using System Center Configuration Manager](../../core/servers/deploy/start-using.md)
