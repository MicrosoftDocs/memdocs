---
title: Migration operations
titleSuffix: Configuration Manager
description: Create and run jobs to migrate data and clients to Configuration Manager current branch.
ms.date: 12/30/2016
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
# Operations for migrating to Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

For migration in Configuration Manager, you can migrate data and clients after you successfully gather data from a source site in a supported source hierarchy. Use the information in the following sections to create and run migration jobs to migrate data and clients, and then finish the migration process.  

-   [Create and edit migration jobs](#Create_Edit_migration_Jobs)  

-   [Run migration jobs](#Run_Migration_Jobs)  

-   [Upgrade or reassign a shared distribution point](#BKMK_ProcUpgrdSS)  

-   [Monitor migration activity in the Migration workspace](#Monitor_MIgration)  

-   [Migrate clients](#BKMK_MigrateClients)  

-   [Finish migration](#Complete_Migration)  

##  <a name="Create_Edit_migration_Jobs"></a> Create and edit migration jobs  
 Use the following procedures to create data migration jobs, edit the exclusion list for collection-based migration jobs, set up shared distribution points, and edit migration job schedules.  

> [!NOTE]  
>  The following procedure for creating a migrating job that migrates by collections applies only to source hierarchies that run a supported version of Configuration Manager 2007. The collection-based migration job type is not available when you migrate from a System Center 2012 Configuration Manager or Configuration Manager current branch source hierarchy.  

#### Create a migration job to migrate by collections  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Migration Jobs**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Migration Job**.  

4.  On the **General** page of the Create Migration Job wizard, set up the following and then choose **OK**:  

    -   Specify a name for the migration job.  

    -   In the **Job type** drop-down list, select **Collection migration**.  

5.  On the **Select Collections** page, set up the following and then choose **Next**:  

    -   Select the collections that you want to migrate.  

    -   If you want to migrate only collections and not the objects that are associated with those collections, uncheck **Migrate objects that are associated with the specified collections**. If you uncheck this option, no associated objects are migrated in this job, and you can skip steps 6 and 7.  

6.  On the **Select Objects** page, uncheck any object types or specific available objects that you do not want to migrate. By default, all associated object types and available objects are selected. Choose **Next**.  

7.  On the **Content Ownership** page, assign the ownership of content from each listed source site to a site in the destination hierarchy, and then choose **Next**.  

8.  On the **Security Scope** page, select one or more role-based administration security scopes to assign to the objects to migrate in this migration job, and then choose **Next**.  

9. On the **Collection Limiting** page, set up a collection from the destination hierarchy to limit the scope of each listed collection, and then choose **Next**. If no collections are listed, choose **Next**.  

10. On the **Site Code Replacement** page, assign a site code from the destination hierarchy to replace the Configuration Manager 2007 site code for each listed collection, and then choose **Next**. If no collections are listed, choose **Next**.  

11. On the **Review Information** page, choose **Save To File** to save the displayed information for later viewing. When you are ready to continue, choose **Next**.  

12. On the **Settings** page, set up when the migration job will run, choose any additional settings that you need for this migration job, and then choose **Next**.  

13. Confirm the settings and finish the wizard.  

#### Create a migration Job to migrate by objects  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Migration Jobs**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Migration Job**.  

4.  On the **General** page of the Create Migration Job wizard, set up the following, and then choose **Next**:  

    -   Specify a name for the migration job.  

    -   In the **Job type** drop-down list, select **Object migration**.  

5.  On the **Select Objects** page, select the object types that you want to migrate. By default, all available objects are selected for each object type that you select.  

6.  On the **Content Ownership** page, assign the ownership of content from each listed source site to a site in the destination hierarchy, and then choose **Next**. If no source sites are listed, choose **Next**.  

7.  On the **Security Scope** page, select one or more role-based administration security scopes to assign to the objects in this migration job, and then choose **Next**.  

8.  On the **Review Information** page, choose **Save To File** to save the displayed information for later viewing. When you are ready to continue, choose **Next**.  

9. On the **Settings** page, set up when the migration job will run and choose any additional settings that you need for this migration job. Then choose **Next**.  

10. Confirm the settings and finish the wizard.  

#### Create a migration job to migrate changed objects  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Migration Jobs**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Migration Job**.  

4.  On the **General** page of the Create Migration Job wizard, set up the following and then choose **Next**:  

    -   Specify a name for the migration job.  

    -   In the **Job type** drop-down list, select **Objects modified after migration**.  

5.  On the **Select Objects** page, select the object types that you want to migrate. By default, all available objects are selected for each object type that you select.  

6.  On the **Content Ownership** page, assign the ownership of content from each listed source site to a site in the destination hierarchy, and then choose **Next**. If no source sites are listed, choose **Next**.  

7.  On the **Security Scope** page, select one or more role-based administration security scopes to assign to the objects in this migration job, and then choose **Next**.  

8.  On the **Review Information** page, choose **Save To File** to save the displayed information for later viewing. When you are ready to continue, choose **Next**.  

9. On the **Settings** page, set up when the migration job will run and choose any additional settings that you require for this migration job. Unlike the other migration job types, this migration job must overwrite the previously migrated objects in the Configuration Manager database. Choose **Next**.  

10. Confirm the settings and then finish the wizard.  

###  <a name="BKMK_Modify_Exclusion_List"></a> Modify the exclusion list for migration  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, choose **Migration** to gain access to the exclusion list. You can also access the exclusion list from the **Source Hierarchy** or **Migration Jobs** node.  

3.  On the **Home** tab, in the **Migration** group, choose **Edit Exclusion List**.  

4.  In the **Edit Exclusion List** dialog box, select the excluded object that you want to remove from the exclusion list, and then choose **Remove**.  

5.  Choose **OK** to save the changes and finish the edit. To cancel current changes and restore all the objects that you have removed, choose **Cancel**, and then choose **No**. This will cancel the removal of the objects, and close the **Edit Exclusion List** dialog box.  

#### Share distribution points from the source hierarchy  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, choose **Source Hierarchy**, and then select the source site that you want to set up.  

3.  On the **Home** tab, in the **Source Site** group, choose **Configure**.  

4.  On the **Source Site Credentials** dialog box, select **Enable distribution point sharing for the source site server**, and then choose **OK**.  

5.  When data gathering finishes, choose **Close**.  

#### Change the schedule of a migration job  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Migration Jobs**.  

3.  Choose the migration job that you want to change. On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  In the properties of the migration job, select the **Settings** tab, change the run time for the migration job, and then choose **OK**.  

##  <a name="Run_Migration_Jobs"></a> Run migration jobs  
 Use the following procedure to run a migration job that has not yet started.  


1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Migration Jobs**.  

3.  Choose the migration job that you want to run. On the **Home** tab, in the **Migration Job** group, choose **Start**.  

4.  Choose **Yes** to start the migration job.  

##  <a name="BKMK_ProcUpgrdSS"></a> Upgrade or reassign a shared distribution point  
 You can upgrade a supported distribution point that is shared from a Configuration Manager 2007 source site (or reassign a supported distribution point that is shared from a Configuration Manager source site) to be a distribution point in the destination hierarchy.  

> [!IMPORTANT]  
>  Before you upgrade a Configuration Manager 2007 branch distribution point, you must uninstall the Configuration Manager 2007 client software from the branch distribution point computer. If the Configuration Manager 2007 client software is installed when you attempt to upgrade the distribution point, the upgrade fails and content that was previously deployed to the branch distribution point is removed from the computer.  

> [!CAUTION]  
>  When you upgrade or reassign a shared distribution point, the distribution point site system role and site system computer are removed from the source site and added as a distribution point to the site in the destination hierarchy that you select.  

#### Upgrade or reassign a shared distribution point  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Source Hierarchy**.  

3.  Select the site that owns the distribution point you want to upgrade, choose the **Shared Distribution Points** tab, and select the eligible distribution point that you want to upgrade or reassign.  

4.  On the **Distribution Point** tab, in the **Distribution Point** group, choose **Reassign**.  

5.  Specify settings in the Reassign Shared Distribution Point wizard like you are installing a new distribution point for the destination hierarchy, with the following addition:  

    -   On the **Content Conversion** page, review the guidance about the space required to convert the existing content. Then, on the **Drive Settings** page of the wizard, ensure that the drive of the distribution point computer that is selected has the required amount of free disk space.  

6.  Confirm the settings and then finish the wizard.  

##  <a name="Monitor_MIgration"></a> Monitor migration activity in the Migration workspace  
 Use the Configuration Manager console to monitor migration.  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Migration Jobs**.  

3.  Choose the migration job that you want to monitor.  

4.  View details and status about the selected migration job on the tabs for **Summary** and **Objects in Job**.  

##  <a name="BKMK_MigrateClients"></a> Migrate clients  
 After you migrate data for clients between hierarchies but before you finish migration, plan to migrate clients to the destination hierarchy. The migration of clients between hierarchies involves uninstalling the Configuration Manager client software from computers that are assigned to the source hierarchy, and then installing the Configuration Manager client software from the destination hierarchy. When you install the client from the destination hierarchy you also assign the client to a primary site in that hierarchy. For more about migrating clients, see [Planning a client migration strategy](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="Complete_Migration"></a> Finish migration  
 Use this procedure to finish migration from the source hierarchy.  

1.  In the Configuration Manager console, choose **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then choose **Source Hierarchy**.  

3.  For a Configuration Manager 2007 source hierarchy, select a source site that is at the bottom level of the source hierarchy. For a System Center 2012 Configuration Manager or Configuration Manager current branch source hierarchy, select the available source site.  

4.  On the **Home** tab, in the **Clean Up** group, choose **Stop Gathering Data**.  

5.  Choose **Yes** to confirm the action.  

6.  For a Configuration Manager 2007 source hierarchy, before you continue to the next step, repeat steps 3, 4, and 5. Go through these steps at each site in the hierarchy, from the bottom of the hierarchy to the top. For a System Center 2012 Configuration Manager or Configuration Manager current branch source hierarchy, continue to the next step.  

7.  On the **Home** tab, in the **Clean Up** group, choose **Clean Up Migration Data**.  

8.  On the **Clean Up Migration Data** dialog box, from the **Source hierarchy** drop-down list, select the site code and site server of the top-level site of the source hierarchy, and then choose **OK**.  

9. Choose **Yes** to finish the migration process for the source hierarchy.  
