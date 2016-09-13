---
title: "Operations for migrating to System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: 6
author: Brenduns
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Operations for migrating to System Center Configuration Manager
For migration in System Center Configuration Manager, after you successfully gather data from a source site in a supported source hierarchy, you can start to migrate data and clients. Use the information in the following sections to create and run migration jobs to migrate data, clients, and to then complete the migration process.  

-   [Create and edit migration jobs](#Create_Edit_migration_Jobs)  

-   [Run migration jobs](#Run_Migration_Jobs)  

-   [Upgrade or reassign a shared distribution point](#BKMK_ProcUpgrdSS)  

-   [Monitor migration activity in the Migration workspace](#Monitor_MIgration)  

-   [Migrate clients](#BKMK_MigrateClients)  

-   [Complete migration](#Complete_Migration)  

##  <a name="Create_Edit_migration_Jobs"></a> Create and edit migration jobs  
 Use the following procedures to create data migration jobs, edit the exclusion list for collection-based migration jobs, configure shared distribution points, and edit migration job schedules.  

> [!NOTE]  
>  The following procedure for creating a migrating job that migrates by collections, applies only for source hierarchies that run a supported version of Configuration Manager 2007. The collection-based migration job type is not available when you migrate from a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy.  

#### To create a migration job to migrate by collections  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Migration Jobs**.  

3.  On the **Home** tab, in the **Create** group, click **Create Migration Job**.  

4.  On the **General** page of the Create Migration Job Wizard configure the following, and then click **OK**:  

    -   Specify a name for the migration job.  

    -   In the **Job type** drop-down list, select **Collection migration**.  

5.  On the **Select Collections** page, configure the following, and then click **Next**:  

    -   Select the collections that you want to migrate.  

    -   If you want to migrate collections only and not the objects that are associated with those collections, clear the **Migrate objects that are associated with the specified collections** option. If you clear this option, no associated objects are migrated in this job, and you can skip steps 6 and 7.  

6.  On the **Select Objects** page, clear any object types, or specific available objects that you do not want to migrate. By default, all associated object types and available objects are selected. Then click **Next**.  

7.  On the **Content Ownership** page, assign the ownership of content from each listed source site to a site in the destination hierarchy, and then click **Next**.  

8.  On the **Security Scope** page, select one or more role-based administration security scopes to assign to the objects to migrate in this migration job, and then click **Next**.  

9. On the **Collection Limiting** page, configure a collection from the destination hierarchy to limit the scope of each listed collection, and then click **Next**. Or, if no collections are listed, click **Next**.  

10. On the **Site Code Replacement** page, assign a site code from the destination hierarchy to replace the Configuration Manager 2007 site code for each listed collection, and then click **Next**. Or, if no collections are listed, click **Next**.  

11. On the **Review Information** page, click **Save To File** to save the displayed information for later viewing. When you are ready to continue, click **Next**.  

12. On the **Settings** page, configure when the migration job will run and any additional settings that you need for this migration job, and then click **Next**.  

13. Confirm the settings and complete the wizard.  

#### To create a migration Job to migrate by objects  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Migration Jobs**.  

3.  On the **Home** tab, in the **Create** group, click **Create Migration Job**.  

4.  On the **General** page of the Create Migration Job Wizard, configure the following, and then click **Next**:  

    -   Specify a name for the migration job.  

    -   In the **Job type** drop-down list, select **Object migration**.  

5.  On the **Select Objects** page, select the object types that you want to migrate. By default, all available objects are selected for each object type that you select.  

6.  On the **Content Ownership** page, assign the ownership of content from each listed source site to a site in the destination hierarchy, and then click **Next**. Or, if no source sites are listed, click **Next**.  

7.  On the **Security Scope** page, select one or more role-based administration security scopes to assign to the objects in this migration job, and then click **Next**.  

8.  On the **Review Information** page, click **Save To File** to save the displayed information for later viewing. When you are ready to continue, click **Next**.  

9. On the **Settings** page, configure when the migration job will run and any additional settings that you need for this migration job. Then click **Next**.  

10. Confirm the settings and complete the wizard.  

#### To create a migration job to migrate changed objects  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Migration Jobs**.  

3.  On the **Home** tab, in the **Create** group, click **Create Migration Job**.  

4.  On the **General** page of the Create Migration Job Wizard, configure the following and then click **Next**:  

    -   Specify a name for the migration job.  

    -   In the **Job type** drop down list, select **Objects modified after migration**.  

5.  On the **Select Objects** page, select the object types that you want to migrate. By default, all available objects are selected for each object type that you select.  

6.  On the **Content Ownership** page, assign the ownership of content from each listed source site to a site in the destination hierarchy, and then click **Next**. Or, if no source sites are listed, click **Next**.  

7.  On the **Security Scope** page, select one or more role-based administration security scopes to assign to the objects in this migration job, and then click **Next**.  

8.  On the **Review Information** page, click **Save To File** to save the displayed information for later viewing. When you are ready to continue, click **Next**.  

9. On the **Settings** page, configure when the migration job will run and any additional settings that you require for this migration job. Unlike the other migration job types, this migration job must overwrite the previously migrated objects in the System Center Configuration Manager database. Click **Next**.  

10. Confirm the settings and then complete the wizard.  

###  <a name="BKMK_Modify_Exclusion_List"></a> To modify the exclusion list for migration  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Migration** to gain access to the exclusion list. You can also access the exclusion list from the **Source Hierarchy** or **Migration Jobs** node.  

3.  On the **Home** tab, in the **Migration** group, click **Edit Exclusion List**.  

4.  On the **Edit Exclusion List** dialog box, select the excluded object that you want to remove from the exclusion list, and then click **Remove**.  

5.  Click **OK** to save the changes and complete the edit. To cancel current changes and restore all the objects that you have removed, click **Cancel**, and then click **No**. This will cancel the removal of the objects, and close the **Edit Exclusion List** dialog box.  

#### To share distribution points from the source hierarchy  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, click **Source Hierarchy**, and then select the source site that you want to configure.  

3.  On the **Home** tab, in the **Source Site** group, click **Configure**.  

4.  On the **Source Site Credentials** dialog box, select **Enable distribution point sharing for the source site server**, and then click **OK**.  

5.  When data gathering finishes, click **Close**.  

#### To change the schedule of a migration job  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Migration Jobs**.  

3.  Click the migration job that you want to modify. On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  In the properties of the migration job, select the **Settings** tab, change the run time for the migration job, and then click **OK**.  

##  <a name="Run_Migration_Jobs"></a> Run migration jobs  
 Use the following procedure to run a migration job that has not yet started.  

#### To run migration jobs  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Migration Jobs**.  

3.  Click the migration job that you want to run. On the **Home** tab, in the **Migration Job** group, click **Start**.  

4.  Click **Yes** to start the migration job now.  

##  <a name="BKMK_ProcUpgrdSS"></a> Upgrade or reassign a shared distribution point  
 You can upgrade a supported distribution point that is shared from a Configuration Manager 2007 source site, or reassign a supported distribution point that is shared from a System Center Configuration Manager source site, to be a distribution point in the destination hierarchy.  

> [!IMPORTANT]  
>  Before you upgrade a Configuration Manager 2007 branch distribution point, you must uninstall the Configuration Manager 2007 client software from the branch distribution point computer. If the Configuration Manager 2007 client software is installed when you attempt to upgrade the distribution point, the upgrade fails and content that was previously deployed to the branch distribution point is removed from the computer.  

> [!CAUTION]  
>  When you upgrade or reassign a shared distribution point, the distribution point site system role and site system computer is removed from the source site and added as a distribution point to the site in the destination hierarchy that you select.  

#### To upgrade or reassign a shared distribution point  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Source Hierarchy**.  

3.  Select the site that owns the distribution point you want to upgrade, click the **Shared Distribution Points** tab, and select the eligible distribution point that you want to upgrade or reassign.  

4.  On the **Distribution Point** tab, in the **Distribution Point** group, click **Reassign**.  

5.  Specify settings in the Reassign Shared Distribution Point Wizard as if you are installing a new distribution point for the destination hierarchy, with the following addition:  

    -   On the **Content Conversion** page, review the guidance about the required space to convert the existing content. Then, on the **Drive Settings** page of the wizard, ensure that the drive of the distribution point computer that is selected contains the required amount of free disk space.  

6.  Confirm the settings and then complete the wizard.  

##  <a name="Monitor_MIgration"></a> Monitor migration activity in the Migration workspace  
 Use the following procedure to use the Configuration Manager console to monitor migration.  

#### To monitor migration activity in the Migration workspace  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Migration Jobs**.  

3.  Click the migration job that you want to monitor.  

4.  View details and status about the selected migration job on the tabs for **Summary** and **Objects in Job**.  

##  <a name="BKMK_MigrateClients"></a> Migrate clients  
 After you migrate data for clients between hierarchies but before you complete migration, plan to migrate clients to the destination hierarchy. The migration of clients between hierarchies involves uninstalling the Configuration Manager client software from computers that are assigned to the source hierarchy, and then installing the Configuration Manager client software from the destination hierarchy. When you install the client from the destination hierarchy you also assign the client to a primary site in that hierarchy. For more information about migrating clients, see [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="Complete_Migration"></a> Complete migration  
 Use this procedure to complete migration from the source hierarchy.  

#### To complete migration  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Source Hierarchy**.  

3.  For a Configuration Manager 2007 source hierarchy, select a source site that is at the bottom level of the source hierarchy. For a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy, select the available source site.  

4.  On the **Home** tab, in the **Clean Up** group, click **Stop Gathering Data**.  

5.  Click **Yes** to confirm the action.  

6.  For a Configuration Manager 2007 source hierarchy, before you continue to the next step, repeat steps 3, 4, and 5. Perform these steps at each site in the hierarchy, from the bottom of the hierarchy to the top. For a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy, continue to the next step.  

7.  On the **Home** tab, in the **Clean Up** group, click **Clean Up Migration Data**.  

8.  On the **Clean Up Migration Data** dialog box, from the **Source hierarchy** drop-down list, select the site code and site server of the top-level site of the source hierarchy, and then click **OK**.  

9. Click **Yes** to complete the migration process for the source hierarchy.  
  
