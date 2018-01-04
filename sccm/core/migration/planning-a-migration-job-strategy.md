---
title: "Migration job planning"
titleSuffix: "Configuration Manager"
description: "Use migration jobs to configure data that you want to migrate to your System Center Configuration Manager environment."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
caps.latest.revision: 6
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe
robots: noindex

---
# Plan a migration job strategy in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use migration jobs to configure the specific data that you want to migrate to your System Center Configuration Manager environment. Migration jobs identify the objects that you plan to migrate, and they run at the top-level site in your destination hierarchy. You can set up one or more migration jobs per source site. This lets you migrate all objects at one time or limited subsets of data with each job.  

 You can create migration jobs after Configuration Manager has successfully gathered data from one or more sites from the source hierarchy. You can migrate data in any sequence from the source sites that have gathered data. With a Configuration Manager 2007 source site, you can migrate data only from the site where an object was created. With source sites that run System Center 2012 Configuration Manager or later, all data that you can migrate is available at the top-level site of the source hierarchy.  

 Before you migrate clients between hierarchies, ensure that the objects that clients use have migrated and that these objects are available in the destination hierarchy. For example, when you migrate from a Configuration Manager 2007 SP2 source hierarchy, you might have an advertisement for content that is deployed to a custom collection that has a client. In this scenario, we recommend that you migrate the collection, the advertisement, and the associated content before you migrate the client. This data cannot be associated with the client in the destination hierarchy if the content, collection, and advertisement are not migrated before the client migrates. If a client is not associated with the data related to a previously run advertisement and content, the client can be offered the content for installation in the destination hierarchy, which might be unnecessary. When the client migrates after the data has migrated, the client is associated with this content and advertisement, and unless the advertisement is recurring, is not offered this content for the migrated advertisement again.  

 Some objects require more than the migration of data from the source hierarchy to the destination hierarchy. For example, to successfully migrate software updates for your clients to your destination hierarchy, you must deploy an active software update point, configure the catalog of products, and synchronize the software update point with Windows Server Update Services (WSUS) in the destination hierarchy.  

 Use the following sections to help you plan your migration jobs.  

-   [Types of migration jobs](#Types_of_Migration)  

-   [General planning for all migration jobs](#About_Migration_Jobs)  

-   [Planning for collection migration jobs](#About_Collection_Migration)  

-   [Planning for object migration jobs](#About_Object_Migration)  

-   [Planning for previously migrated object migration jobs](#About_Object_Migrations)  

##  <a name="Types_of_Migration"></a> Types of migration jobs  
 Configuration Manager supports the following types of migration jobs. Each job type is designed to help define the objects that you can include in that job.  

 **Collection migration** (only supported when migrating from Configuration Manager 2007 SP2): Migrate objects that are related to collections you select. By default, collection migration includes all objects that are associated with members of the collection. You can exclude specific object instances when you use a collection migration job.  

 **Object migration**: Migrate individual objects that you select. You select only the specific data that you want to migrate.  

 **Previously migrated object migration**: Migrate objects that you previously migrated when they have updated in the source hierarchy after they were last migrated.  

###  <a name="Objects_that_can_migrate"></a> Objects that you can migrate  
 Not every object can migrate by a specific type of migration job. The following list identifies the type of objects that you can migrate with each type of migration job.  

> [!NOTE]  
>  Collection migration jobs are available only when you migrate objects from a Configuration Manager 2007 SP2 source hierarchy.  

 **Job types you can use to migrate each object**  

-   **Advertisements** (available to migrate from supported Configuration Manager 2007 source sites)  

    -   Collection migration  


-   **Asset Intelligence catalog**  

    -   Object migration  

    -   Previously migrated object migration  

-   **Asset Intelligence hardware requirements**  

    -   Object migration  

    -   Previously migrated object migration  

-   **Asset Intelligence software list**  

    -   Object migration  

    -   Previously migrated object migration  

-   **Boundaries**  

    -   Object migration  

    -   Previously migrated object migration  

-   **Configuration baselines**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Configuration items**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Maintenance windows**  

    -   Collection migration  


-   **Operating system deployment boot images**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Operating system deployment driver packages**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Operating system deployment drivers**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Operating system deployment images**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Operating system deployment packages**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Software distribution packages**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Software metering rules**  

    -   Object migration  

    -   Previously migrated object migration  

-   **Software update deployment packages**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Software update deployment templates**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Software update deployments**  

    -   Collection migration  


-   **Software update lists**  

    -   Object migration  

    -   Previously migrated object migration  

-   **Task sequences**  

    -   Collection migration  

    -   Object migration  

    -   Previously migrated object migration  

-   **Virtual application packages**  

    -   Collection migration  

    -   Object migration  

    > [!IMPORTANT]  
    >  Although you can migrate a virtual application package by using object migration, the packages cannot be migrated by using the migration job type of **Previously Migrated Object Migration**. Instead, you must delete the migrated virtual application package from the destination site and then create a new migration job to migrate the virtual application.  

##  <a name="About_Migration_Jobs"></a> General planning for all migration jobs  
 Use the Create Migration Job wizard to create a migration job to migrate objects to your destination hierarchy. The type of the migration job that you create determines which objects are available to migrate. You can create and use multiple migration jobs to migrate data from the same source site or from multiple source sites. The use of one type of migration job does not block the use of a different type of migration job.  

 After a migration job runs successfully, its status is listed as **Completed** and it cannot be run again. However, you can create a new migration job to migrate any of the objects that were migrated by the original job, and the new migration job can include additional objects as well. When you create additional migration jobs, the objects that have been previously migrated show the state of **Migrated**. You can select these objects to migrate them again, but unless the object has been updated in the source hierarchy, migrating these objects again is not necessary. If the object has been updated in the source hierarchy after it was originally migrated, you can identify that object when you use the migration job type of **Objects modified after migration**.  

 You can delete a migration job before it runs. However, after a migration job finishes, it remains visible in the Configuration Manager console and cannot be deleted. Each migration job that has finished or has not yet run remains visible in the Configuration Manager console until you finish the migration process and clean up migration data.  

> [!NOTE]  
>  After you have finished migration by using the **Clean Up Migration Data** action, you can reconfigure the same hierarchy as the current source hierarchy to restore visibility to the objects you previously migrated.  

 You can view the objects contained in any migration job in the Configuration Manager console by selecting the migration job and then choosing the **Objects in Job** tab.  

 Use the information in the following sections to help you plan for all migration jobs.  

### Data selection  
 When you create a collection migration job, you must select one or more collections. After you select the collections, the Create Migration Job wizard shows the objects that are associated with the collections. By default, all objects associated with the selected collections are migrated, but you can uncheck the objects that you do not want to migrate with that job. When you uncheck an object that has dependent objects, those dependent objects are also unchecked. All unchecked objects are added to an exclusion list. Objects on an exclusion list are removed from automatic selection for future migration jobs. You must manually edit the exclusion list to remove objects that you want to have automatically selected for migration in migration jobs you create in the future.  

### Site ownership for migrated content  
 When you migrate content for deployments, you must assign the content object to a site in the destination hierarchy. This site then becomes the owner for that content in the destination hierarchy. Although the top-level site of your destination hierarchy is the site that actually migrates the metadata for content, it is the assigned site that accesses the original source files for the content across the network.  

 To minimize the network bandwidth that is used during migration, consider transferring ownership of content to the closest available site. Because information about the content is shared globally in System Center Configuration Manager, it will be available at every site.  

 Information about content is shared to all sites in the destination hierarchy by using database replication. However, any content that you assign to a primary site and then deploy to distribution points at other primary sites transfers by using file-based replication. This transfer is routed through the central administration site and then to each additional primary site. By centralizing packages that you plan to distribute to multiple primary sites before or during migration when you assign a site as the content owner, you can reduce data transfers across low-bandwidth networks.  

### Role-based administration security scopes for migrated data  
 When you migrate data to a destination hierarchy, you must assign one or more role-based administration security scopes to the objects whose data is migrated. This ensures that only the appropriate administrative users have access to this data after it is migrated. The security scopes that you specify are defined by the migration job and are applied to each object that is migrated by that job. If you require different security scopes to be applied to different sets of objects and you want to assign those scopes during migration, you must migrate the different sets of objects by using different migration jobs.  

 Before you set up a migration job, review how role-based administration works in System Center Configuration Manager. If necessary, set up one or more security scopes for the data that you migrate to control who will have access to the migrated objects in the destination hierarchy.  

 For more about security scopes and role-based administration, see [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### Review migration actions  
 When you set up a migration job, the Create Migration Job wizard shows a list of actions that you must take to ensure a successful migration and a list of actions that Configuration Manager takes during the migration of the selected data. Review this information carefully to check the expected outcome.  

### Schedule migration jobs  
 By default, a migration job runs immediately after it is created. However, you can specify when the migration job runs when you create the job or by editing the properties of the job. You can schedule the migration job to run as follows:  

-   Run the job now  

-   Run the job at a specific start time  

-   Not run the job  

### Specify conflict resolution for migrated data  
 By default, migration jobs do not overwrite data in the destination database unless you configure the migration job to skip or overwrite data that has previously been migrated to the destination database.  

##  <a name="About_Collection_Migration "></a> Plan for collection migration jobs  
 Collection migration jobs are available only when you migrate data from a source hierarchy that runs a supported version of Configuration Manager 2007. You must specify one or more collections to migrate when you migrate by collection. For each collection that you specify, the migration job automatically selects all related objects for migration. For example, if you select a specific collection of users, the collection members are then identified, and you can migrate the deployments associated with that collection. Optionally, you can select other deployment objects to migrate that are associated with those members. All these selected items are added to the list of objects that can be migrated.  

 When you migrate a collection, System Center Configuration Manager also migrates collection settings, including maintenance windows and collection variables, but it cannot migrate collection settings for AMT client provisioning.  

 Use the information in the following sections to learn about additional configurations that can apply to collection-based migration jobs.  

### Exclude objects from collection migration jobs  
 You can exclude specific objects from a collection migration job. When you exclude a specific object from a collection migration job, that object is added to a global exclusion list that has all the objects that you have excluded from migration jobs created for any source site in the current source hierarchy. Objects on the exclusion list are still available for migration in future jobs but are not automatically included when you create a new collection-based migration job.  

 You can edit the exclusion list to remove objects that you have previously excluded. After you remove an object from the exclusion list, it is then automatically selected when an associated collection is specified during the creation of a new migration job.  

### Unsupported collections  
 Configuration Manager can migrate any of the default user collections, device collections, and most custom collections from a Configuration Manager 2007 source hierarchy. However, Configuration Manager cannot migrate collections that contain users and devices in the same collection.  

 The following collections cannot be migrated:  

-   A collection that has users and devices.  

-   A collection that has a reference to a collection of a different resource type. For example, a device-based collection that has either a subcollection or a link to a user-based collection. In this example, only the top-level collection migrates.  

-   A collection that has a rule to include unknown computers. The collection migrates, but the rule to include unknown computers does not migrate.  

### Empty collections  
 An empty collection is a collection that has no resources associated with it. When Configuration Manager migrates an empty collection, it converts the collection to an organizational folder that has no users or devices. This folder is created with the name of the empty collection under the **User Collections** or **Device Collections** node in the **Assets and Compliance** workspace in the Configuration Manager console.  

### Linked collections and subcollections  
 When you migrate collections that are linked to other collections or that have subcollections, Configuration Manager creates a folder under the **User Collections** or **Device Collections** node in addition to the linked collections and subcollections.  

### Collection dependencies and include objects  
 When you specify a collection to migrate in the Create Migration Job wizard, any dependent collections are automatically selected to be included with the job. This behavior ensures that all necessary resources are available after migration.  

 For example: You select a collection for devices that run Windows 7 and is named **Win_7**. This collection is limited to a collection that has all your client operating systems and is named **All_Clients**. The collection **All_Clients** will be automatically selected for migration.  

### Collection limiting  
 With System Center Configuration Manager, collections are global data and are evaluated at each site in the hierarchy. Therefore, plan how to limit the scope of a collection after it is migrated. During migration, you can identify a collection from the destination hierarchy to use to limit the scope of the collection that you are migrating so that the migrated collection does not include unanticipated members.  

 For example, in Configuration Manager 2007, collections are evaluated at the site that creates them and at child sites. An advertisement might be deployed to only a child site, and this would limit the scope for that advertisement to that child site. In comparison, with System Center Configuration Manager, collections are evaluated at each site and associated advertisements are then evaluated for each site. Collection limiting lets you refine the collection members based on another collection to avoid the addition of unexpected collection members.  

### Site code replacement  
 When you migrate a collection that has criteria that identifies a Configuration Manager 2007 site, you must specify a specific site in the destination hierarchy. This ensures that the migrated collection remains functional in your destination hierarchy and does not increase in scope.  

### Specify behavior for migrated advertisements  
 By default, collection-based migration jobs disable advertisements that migrate to the destination hierarchy. This includes any programs that are associated with the advertisement. When you create a collection-based migration job that has advertisements, you see the **Enable programs for deployment in Configuration Manager after an advertisement is migrated** option on the **Settings** page of the Create Migration Job wizard. If you select this option, programs that are associated with the advertisements are enabled after they have migrated. As a best practice, do not select this option. Instead, enable the programs after they have migrated when you can verify the clients that will receive them.  

> [!NOTE]  
>  You see the **Enable programs for deployment in Configuration Manager after an advertisement is migrated** option only when you are creating a collection-based migration job and the migration job contains advertisements.  

 To enable a program after migration, clear **Disable this program on computers where it is advertised** on the **Advanced** tab of the program properties.  

##  <a name="About_Object_Migration"></a> Plan for object migration jobs  
 Unlike collection migration, you must select each object and object instance that you want to migrate. You can select the individual objects (like advertisements from a Configuration Manager 2007 hierarchy or a publication from a System Center 2012 Configuration Manager or System Center Configuration Manager hierarchy) to add to the list of objects to migrate for a specific migration job. Any objects that you do not add to the migration list are not migrated to the destination site by the object migration job.  

 Object-based migration jobs do not have any additional configurations to plan for beyond those applicable to all migration jobs.  

##  <a name="About_Object_Migrations"></a> Plan for previously migrated object migration jobs  
 When an object that you have already migrated to the destination hierarchy is updated in the source hierarchy, you can migrate that object again by using the **Objects modified after migration** job type. For example, when you rename or update the source files for a package in the source hierarchy, the package version increments in the source hierarchy. After the package version increments, the package can be identified for migration by this job type.  

 This job type is similar to the object migration type except that when you select objects to migrate, you can only select from objects that have been updated after they were migrated by a previous migration job.   

 When you select this job type, the conflict resolution behavior on the **Settings** page of the Create Migration Job wizard is configured to overwrite previously migrated objects. This setting cannot be changed.  

> [!NOTE]  
>  This migration job can identify objects that are automatically updated by the source hierarchy and objects that an administrative user updates.  
