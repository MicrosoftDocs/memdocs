---
title: "Migrate objects"
description: "Learn how to plan for the migration of objects between hierarchies in a System Center Configuration Manager environment."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Plan for the migration of Configuration Manager objects to System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With System Center Configuration Manager, you can migrate many of the different objects that are associated with different features found at a source site. Use the following sections to help you plan for the migration of objects between hierarchies.  

-   [Plan to migrate software updates](#Plan_migrate_Software_updates)  

-   [Plan to migrate content](#Plan_Migrate_content)  

-   [Plan to migrate collections](#BKMK_MigrateCollections)  

-   [Plan to migrate operating system deployments](#Plan_migrate_OSD)  

-   [Plan to migrate desired configuration management](#Plan_Migrate_Compliance_settings)  

-   [Plan to migrate boundaries](#Plan_migrate_Boundaries)  

-   [Plan to migrate reports](#Plan_Migrate_reports)  

-   [Plan to migrate organizational and search folders](#Plan_Migrate_Org_Folders)  

-   [Plan to migrate Asset Intelligence customizations](#Plan_Migrate_AI)  

-   [Plan to migrate software metering rules customizations](#Plan_Migrate_SWM_Rules)  

##  <a name="Plan_migrate_Software_updates"></a> Plan to migrate software updates  
 You can migrate software update objects, like software update packages and software update deployments.  

 To successfully migrate software update objects, you must first set up your destination hierarchy with configurations that match your source hierarchy environment. This requires the following actions:  

-   Deploy an active software update point in the destination hierarchy  

-   Set up the catalog of products and languages to match the configuration of your source hierarchy  

-   Sync the software update point in the destination hierarchy with Windows Server Update Services (WSUS)  

When you migrate software updates, consider the following:  

-   Migration of software update objects can fail when you have not synced information in your destination hierarchy to match the configuration of your source hierarchy.  

    > [!WARNING]  
    >  Configuration Manager does not support use of the WSUSutil tool to sync data between a source and destination hierarchy.  

-   You cannot migrate custom updates that are published by using System Center Updates Publisher. Instead, custom updates must be republished to the destination hierarchy.  

When you migrate from a Configuration Manager 2007 source hierarchy, the migration process modifies some software update objects to the format in use by the destination hierarchy. Use the following table to help you plan the migration of software update objects from Configuration Manager 2007.  

|Configuration Manager 2007 object|Object name after migration|  
|-----------------------------------|---------------------------------|  
|Software update lists|Software update lists are converted to software update groups.|  
|Software update deployments|Software update deployments are converted to deployments and update groups.<br /><br /> After you migrate a software update deployment from Configuration Manager 2007, you must enable it in the destination hierarchy before you can deploy it.|  
|Software update packages|Software update packages remain software update packages.|  
|Software update templates|Software update templates remain software update templates.<br /><br /> The **Duration** value in Configuration Manager 2007 deployment templates does not migrate.|  

When you migrate objects from a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy, the software updates objects are not modified.  

##  <a name="Plan_Migrate_content"></a> Plan to migrate content  
 You can migrate content from a supported source hierarchy to your destination hierarchy. For a Configuration Manager 2007 source hierarchy, this content includes software distribution packages and programs and virtual applications, like Microsoft Application Virtualization (App-V). For System Center 2012 Configuration Manager and System Center Configuration Manager source hierarchies, this content includes applications and App-V virtual applications. When you migrate content between hierarchies, the compressed source files migrate to the destination hierarchy.  

### Packages and programs  
 When you migrate packages and programs, they are not modified by migration. However, before you migrate them, you must set up each package to use a Universal Naming Convention (UNC) path for its source file location. As part of the configuration to migrate packages and programs, you must assign a site in the destination hierarchy to manage this content. The content is not migrated from the assigned site, but after migration, the assigned site accesses the original source file location by using the UNC mapping.  

 After you migrate a package and program to the destination hierarchy, and while migration from the source hierarchy remains active, you can make the content available to clients in that hierarchy by using a shared distribution point. To use a shared distribution point, the content must remain accessible on the distribution point at the source site. For more about shared distribution points, see [Share distribution points between source and destination hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Plan a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 For content that has migrated, if the content version changes in the source hierarchy or the destination hierarchy, clients can no longer access the content from the shared distribution point in the destination hierarchy. In this scenario, you must re-migrate the content to restore a consistent version of the package between the source hierarchy and the destination hierarchy. This information syncs during the data gathering cycle.  

> [!TIP]  
>  For each package that you migrate, update the package in the destination hierarchy. This action can prevent issues with deploying the package to distribution points in the destination hierarchy. However, when you update a package on the distribution point in the destination hierarchy, clients in that hierarchy will no longer be able to get that package from a shared distribution point. To update a package in the destination hierarchy, in the Configuration Manager console, go to the Software Library, right-click on the package, and then select **Update Distribution Points**. Do this action for each package that you migrate.  

> [!TIP]  
>  You can use Microsoft System Center Configuration Manager Package Conversion Manager to convert packages and programs into System Center Configuration Manager applications. Download Package Conversion Manager from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=212950) site. For more information, see [Configuration Manager Package Conversion Manager](http://go.microsoft.com/fwlink/p/?LinkId=247245).  

### Virtual applications  
When you migrate App-V packages from a supported Configuration Manager 2007 site, the migration process converts them to applications in the destination hierarchy. Additionally, based on existing advertisements for the App-V package, the following deployment types are created in the destination hierarchy:  

-   If there are no advertisements, one deployment type is created that uses the default deployment type settings.  

-   If one advertisement exists, one deployment type is created that uses the same settings as the Configuration Manager 2007 advertisement.  

-   If multiple advertisements exist, a deployment type is created for each Configuration Manager 2007 advertisement by using the settings for that advertisement.  

> [!IMPORTANT]  
>  If you migrate a previously migrated Configuration Manager 2007 App-V package, the migration fails because virtual application packages do not support the overwrite migration behavior. In this scenario, you must delete the migrated virtual application package from the destination hierarchy, and then create a new migration job to migrate the virtual application.  

> [!NOTE]  
>  After you migrate an App-V package, you can use the Update Content wizard to change the source path for App-V deployment types. For more about how to update content for a deployment type, see How to manage deployment types in [Management tasks for System Center Configuration Manager applications](../../apps/deploy-use/management-tasks-applications.md).  

When you migrate from a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy, you can migrate objects for the App-V virtual environment in addition to App-V deployment types and applications. For more about App-V environments, see [Deploying App-V virtual applications with System Center Configuration Manager](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### Advertisements  
You can migrate advertisements from a supported Configuration Manager 2007 source site to the destination hierarchy by using collection-based migration. If you upgrade a client, it retains the history of previously run advertisements to prevent the client from rerunning migrated advertisements.  

> [!NOTE]  
>  You cannot migrate advertisements for virtual packages. This is an exception to the migration of advertisements.  

### Applications  
 You can migrate applications from a supported System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy to a destination hierarchy. If you reassign a client from the source hierarchy to the destination hierarchy, the client retains the history of previously installed applications to prevent the client from rerunning a migrated application.  

##  <a name="BKMK_MigrateCollections"></a> Plan to migrate collections  
 You can migrate the criteria for collections from a supported System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy. For this, you use an object-based migration job. When you migrate a collection, you migrate the rules for the collection and not information about the members of the collection or information or objects related to the members of the collection.  

 Migration of the collection object is not supported when you migrate from a Configuration Manager 2007 source hierarchy.  

##  <a name="Plan_migrate_OSD"></a> Plan to migrate operating system deployments  
You can migrate the following operating system deployment objects from a supported source hierarchy:  

-   Operating system images and packages. The source path of boot images is updated to the default image location for the Windows Administrative Installation Kit (Windows AIK) on the destination site. The following are requirements and limitations to migrating operating system images and packages:  

    -   To successfully migrate image files, the computer account of the SMS Provider server for the destination hierarchy's top-level site must have **Read** and **Write** permission to the image source files of the source site's Windows AIK location.  

    -   When you migrate an operating system installation package, ensure that the configuration of the package on the source site points to the folder that has the WIM file and not to the WIM file itself. If the installation package points to the WIM file, the migration of the installation package will fail.  

    -   When you migrate a boot image package from a Configuration Manager 2007 source site, the package ID of the package is not maintained in the destination site. The result of this is that clients in the destination hierarchy cannot use boot image packages that are available on shared distribution points.  

-   Task sequences. When you migrate a task sequence that has a reference to a client installation package, that reference is replaced with a reference to the client installation package of the destination hierarchy.  

    > [!NOTE]  
    >  When you migrate a task sequence, Configuration Manager might migrate objects that are not required in the destination hierarchy. These objects include boot images and Configuration Manager 2007 client installation packages.  

-   Drivers and driver packages. When you migrate driver packages, the computer account of the SMS Provider in the destination hierarchy must have full control to the package source.

##  <a name="Plan_Migrate_Compliance_settings"></a> Plan to migrate desired configuration management  
You can migrate configuration items and configuration baselines.  

> [!NOTE]  
>  Uninterpreted configuration items from Configuration Manager 2007 source hierarchies are not supported for migration. You cannot migrate or import these configuration items to the destination hierarchy. For more about uninterpreted configuration items, see Uninterpreted configuration items in the [About Configuration Items in Desired Configuration Management](http://go.microsoft.com/fwlink/?LinkId=103846) topic in the Configuration Manager 2007 documentation library.  

You can import Configuration Manager 2007 Configuration Packs. The import process automatically converts the configuration packs to be compatible with System Center Configuration Manager.  

##  <a name="Plan_migrate_Boundaries"></a> Plan to migrate boundaries  
 You can migrate boundaries between hierarchies. When you migrate boundaries from Configuration Manager 2007, each boundary from the source site migrates at the same time and is added to a new boundary group that is created in the destination hierarchy. When you migrate boundaries from a System Center 2012 Configuration Manager or System Center Configuration Manager hierarchy, each boundary you select is added to a new boundary group in the destination hierarchy.  

 Each automatically created boundary group is enabled for content location but not for site assignment. This prevents overlapping boundaries for site assignment between the source and destination hierarchies. When you migrate from a Configuration Manager 2007 source site, this helps prevent new Configuration Manager 2007 clients that install from incorrectly assigning to the destination hierarchy. By default,  System Center Configuration Manager clients do not automatically assign to Configuration Manager 2007 sites.  

 During migration, if you share a distribution point with the destination hierarchy, any boundaries that are associated with that distribution automatically migrate to the destination hierarchy. In the destination hierarchy, migration creates a new read-only boundary group for each shared distribution point. If you change the boundaries for the distribution point in the source hierarchy, the boundary group in the destination hierarchy updates with these changes during the next data gathering cycle.  

##  <a name="Plan_Migrate_reports"></a> Plan to migrate reports  
Configuration Manager does not support the migration of reports. Instead, use SQL Server Reporting Services Report Builder to export reports from the source hierarchy, and then import them to the destination hierarchy.  

> [!NOTE]  
>  Because there are schema changes for reports between Configuration Manager 2007 and System Center Configuration Manager, test each report that you import from a Configuration Manager 2007 hierarchy to ensure that it functions as expected.  

For more about reporting, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="Plan_Migrate_Org_Folders"></a> Plan to migrate organizational and search folders  
 You can migrate organizational folders and search folders from a supported source hierarchy to a destination hierarchy. In addition, from a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy, you can migrate the criteria for a saved search to a destination hierarchy.  

 By default, the migration process maintains your search folder and administrative folder structures for objects and collections when you migrate. However, in the Create Migration Job wizard, on the **Settings** page, you can set up a migration job to not migrate the organizational structure for objects by unchecking the box for this option. The organizational structures of collections are always maintained.  

 One exception to this is a search folder that contains virtual applications. When an App-V package is migrated, the App-V package is transformed into an application in System Center Configuration Manager. After migration of the search folder, only the remaining packages are found, and the search folder cannot locate an App-V package because of this conversion to an application when the App-V package migrates.  

 When you migrate a saved search from a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy, you migrate the criteria for the search, and not the information about the search results. Migration of a saved search is not applicable from a Configuration Manager 2007 source site.  

##  <a name="Plan_Migrate_AI"></a> Plan to migrate Asset Intelligence customizations  
 You can migrate customizations for Asset Intelligence from a supported source hierarchy to a destination hierarchy. There are no significant changes to the structure of Asset Intelligence customizations between Configuration Manager 2007 and System Center Configuration Manager.  

> [!NOTE]  
>  System Center Configuration Manager does not support the migration of Asset Intelligence objects from a Configuration Manager 2007 site that is using Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="Plan_Migrate_SWM_Rules"></a> Plan to migrate software metering rules customizations  
 There are no significant changes to software metering between Configuration Manager 2007 and System Center Configuration Manager. You can migrate your software metering rules from a supported source hierarchy to a destination hierarchy.  

 By default, software metering rules that you migrate to a destination hierarchy are not associated with a specific site in the destination hierarchy and instead apply to all clients in the hierarchy. To apply a software metering rule to clients at a specific site, you must edit the metering rule after it migrates.  
