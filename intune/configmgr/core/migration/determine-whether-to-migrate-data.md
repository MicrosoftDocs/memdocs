---
title: Choose what to migrate
titleSuffix: Configuration Manager
description: Learn which data you can migrate and which data you can't migrate to Configuration Manager current branch.
ms.date: 12/29/2016
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
# Determine whether to migrate data to Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

In Configuration Manager current branch, migration provides a process for transferring data and configurations that you've created from supported versions of Configuration Manager to your new hierarchy.  You can use this to:  

-   Combine multiple hierarchies into one.  

-   Move data and configurations from a lab deployment into your production deployment.

-   Move data and configuration from a prior version of Configuration Manager, like Configuration Manager 2007, which has no upgrade path to Configuration Manager current branch, or from System Center 2012 Configuration Manager (which does support an upgrade path to Configuration Manager current branch).  

With the exception of the distribution point site system role and the computers that host distribution points, no infrastructure (which includes sites, site system roles, or computers that host a site system role), migrates, transfers, or can be shared between hierarchies.  

 Although you cannot migrate server infrastructure, you can migrate Configuration Manager clients between hierarchies. Client migration involves migrating the data that clients use from the source hierarchy to the destination hierarchy, and then installing or reassigning the client software so that the client then reports to the new hierarchy.

After you install a client to the new hierarchy and the client submits its data, its unique Configuration Manager ID helps Configuration Manager associate the data that you previously migrated with each client computer.  

 The functionality that's provided by migration helps you maintain investments that you have made in configurations and deployments while letting you take full advantage of core changes in the product first (which was first introduced in System Center 2012 Configuration Manager and then continued in Configuration Manager). These changes include a simplified Configuration Manager hierarchy that uses fewer sites and resources, and the improved processing that comes from using native 64-bit code that runs on 64-bit hardware.  

 For information about the versions of Configuration Manager that migration supports, see [Prerequisites for migration](../../core/migration/prerequisites-for-migration.md).  

## <a name="Can_Migrate"></a> Data that you can migrate to Configuration Manager current branch

Migration can migrate most objects between supported Configuration Manager hierarchies. The migrated instances of some objects from a supported version of Configuration Manager 2007 must be modified to conform to the System Center 2012 Configuration Manager schema and object format.

These modifications don't affect the data in the source site database. Objects that are migrated from a supported version of System Center 2012 Configuration Manager or Configuration Manager current branch don't require modification.  

The following are objects that can migrate based on the version of Configuration Manager in the source hierarchy. Some objects, like queries, do not migrate. If you want to continue to use these objects that do not migrate you must recreate them in the new hierarchy. Other objects, including some client data, are automatically recreated in the new hierarchy when you manage clients in that hierarchy.  

### Objects that you can migrate from System Center 2012 Configuration Manager or Configuration Manager current branch

-   Applications for System Center 2012 Configuration Manager and later versions  

-   App-V Virtual Environment from System Center 2012 Configuration Manager and later versions  

-   Asset Intelligence customizations  

-   Boundaries  

-   Collections: To migrate collections from a supported version of System Center 2012 Configuration Manager or Configuration Manager current branch, you use an object migration job.  

-   Compliance settings:  

    -   Configuration baselines  

    -   Configuration items  

-   Deployments  

-   Operating system deployment:  

    -   Boot images  

    -   Driver packages  

    -   Drivers  

    -   Images  

    -   Packages  

    -   Task sequences  

-   Search results: Saved search criteria  

-   Software updates:  

    -   Deployments  

    -   Deployment packages  

    -   Templates  

    -   Software update lists  

-   Software distribution packages  

-   Software metering rules  

-   Virtual application packages  

### Objects that you can migrate from Configuration Manager 2007 SP2

-   Advertisements  

-   Applications for System Center 2012 Configuration Manager and later versions  

-   App-V Virtual Environment from System Center 2012 Configuration Manager and later versions  

-   Asset Intelligence customizations  

-   Boundaries  

-   Collections: You migrate collections from a supported version of Configuration Manager 2007 by using a collection migration job.  

-   Compliance settings (referred to as desired configuration management in Configuration Manager 2007):  

    -   Configuration baselines  

    -   Configuration items  

-   Operating system deployment:  

    -   Boot images  

    -   Driver packages  

    -   Drivers  

    -   Images  

    -   Packages  

    -   Task sequences  

-   Search results: Search folders  

-   Software updates:  

    -   Deployments  

    -   Deployment packages  

    -   Templates  

    -   Software update lists  

-   Software distribution packages  

-   Software metering rules  

-   Virtual application packages  

## <a name="Cannot_migrate"></a> Data that you can't migrate to Configuration Manager current branch

You cannot migrate the following types of objects:  

-   AMT client provisioning information  

-   Files on clients, including:  

    -   Client inventory and history data  

    -   Files in the client cache  

-   Queries  

-   Configuration Manager 2007 security rights and instances for the site and objects  

-   Configuration Manager 2007 reports from SQL Server Reporting Services  

-   Configuration Manager 2007 web reports  

-   System Center 2012 Configuration Manager and Configuration Manager current branch reports  

-   System Center 2012 Configuration Manager and Configuration Manager current branch role-based administration:  

    -   Security roles  

    -   Security scopes  
