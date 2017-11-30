---
title: "Migration checklists"
titleSuffix: "Configuration Manager"
description: "Use administrator checklists to help you plan a migration strategy to System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
caps.latest.revision: 7
caps.handback.revision: 0
author: aaroncz
ms.author: aaroncz
manager: angrobe

---
# Administrator checklists for migration planning in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the following administrator checklists to help you plan your migration strategy to System Center Configuration Manager.

##  <a name="Checklist_Migraiton_Planning"></a> Administrator checklist for migration planning  
 Use the following checklist for pre-migration planning steps.  

-   **Assess the current environment:**  

     Identify existing business requirements that are met by the source hierarchy and develop plans to continue to meet those requirements in the destination hierarchy.  

-   **Review the functionality and changes that are available with the version of Configuration Manager that you use, and use this information to help you design your destination hierarchy:**  

    For more information, see [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md) and [What's new in System Center Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Determine the administrative security model to use for role-based administration:**  

    For more information, see [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Assess your network and Active Directory topology:** 
    Review your existing domain structure and network topology and consider how this influences your hierarchy design and migration tasks.  

-   **Finalize your destination hierarchy design:**  

    Decide upon the placement of a central administration site, primary sites, secondary sites, and content distribution options.  

-   **Map your hierarchy to the computers that you will use for sites and site servers in the destination hierarchy:**  

    Identify the computers that sites and site system servers will use in the destination hierarchy, and then ensure that they have sufficient capacity to meet existing and future operational requirements.  

-   **Plan your object migration strategy:**  

    Plan to use the available migration jobs to migrate different objects, including site boundaries, collections, advertisements, and deployments. For more information, see [Types of migration jobs](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) in [Planning a migration job strategy in System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)  

    Configuration Manager migrates only the objects that you select. Any objects that are not migrated and that are required in the destination hierarchy must be re-created in the destination hierarchy.  

    Objects that can migrate are displayed when you configure migration jobs.  

-   **Plan your client migration strategy:**  

    Plan to migrate clients by using a controlled approach that limits the network bandwidth and server processing requirements when you migrate clients to the destination hierarchy. For more about planning a client migration strategy, see [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Plan for inventory and compliance data:**  

    Configuration Manager does not support migrating hardware inventory, software inventory, or desired configuration management compliance data for software updates or clients.  

    Instead, after the client migrates to its new site in the destination hierarchy and receives policy for these configurations, the client submits this information to its assigned site. This action populates the destination site database with current inventory and compliance data.  

-   **Plan for the completion of migration from the source hierarchy:**  

    Decide when objects and clients will be migrated. After migration completes, you can plan to decommission the site servers in the source hierarchy.  

##  <a name="Checklist_Hierarchy_for_migration"></a> Administrator checklist for hierarchy migration  
Use the following checklist to help you plan a destination hierarchy before you start migration.  

-   **Identify the computers to use in the destination hierarchy:**  

    Configuration Manager does not support an in-place upgrade from Configuration Manager 2007 infrastructure. Instead you use migration to move data from Configuration Manager 2007 to System Center Configuration Manager. This requires you to use a side-by-side deployment and install System Center Configuration Manager on new computers.  

    Similarly, when you migrate from another System Center Configuration Manager hierarchy, you must install a new destination hierarchy that is a side-by-side deployment to your source hierarchy.  

-   **Create your destination hierarchy:**  

    To prepare for migration, install and configure a System Center Configuration Manager destination hierarchy that includes a primary site. For example:  

    -   Install a central administration site and then install at least one child primary.  

    -   Install a stand-alone primary if you do not plan to use a central administration site.  

-   **If you want to migrate information that is related to software updates, configure a software update point in the destination hierarchy and synchronize software updates:**  

    You must configure and synchronize software updates in the destination hierarchy before you can migrate software updates information from the source hierarchy.  


-   **Install and configure additional site system roles in the destination hierarchy:**  

    Configure additional site system roles and site systems that you require.  

-   **Check operational functionality in the destination hierarchy:**  

    Check the following:  

    -   If the destination hierarchy includes multiple sites, confirm that database replication is working between sites. Database replication is not applicable to stand-alone primary sites.  

    -   Check that all installed site system roles are operational.  

    -   Check that the Configuration Manager clients you install to the destination hierarchy can communicate successfully with their assigned site.  


##  <a name="Checklisit_Migration"></a> Administrator checklist for migration  
Use the following checklist to migrate data from the source hierarchy to the destination hierarchy.  

-   **Enable migration in the destination hierarchy:**  

    Configure a source hierarchy by specifying the top-level site of the source hierarchy. For more about specifying the source site, see [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **When the source hierarchy runs Configuration Manager 2007 SP2, select and configure additional sites in the source hierarchy:**  

    For each additional site in the Configuration Manager 2007 SP2 source hierarchy that you want to collect data from, you must configure credentials for data gathering. When you configure each source site, the data-gathering process begins immediately and continues throughout the migration period until you stop data gathering for that site. Data gathering ensures that you can migrate objects from the source hierarchy that are updated or added after a previous data-gathering process.

    > [!NOTE]  
    >  When the source hierarchy runs System Center 2012 Configuration Manager or later, you do not need to configure additional source sites.  

-   **Configure distribution point sharing:**  

    You can share distribution points between the two hierarchies to make content for objects that you migrate available to clients in the destination hierarchy. This ensures that the same content remains available for clients in both hierarchies and that you can maintain this content until you stop gathering data and finish the migration.  

    For information about shared distribution points, see [Share distribution points between source and destination hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Create and run migration jobs to migrate objects associated with the clients in the source hierarchy:**  

    Create migration jobs to migrate objects between hierarchies. The required configurations for each migration job can vary depending on what data the job migrates.  

    For example, when you migrate content, regardless of the migration job you use, you must assign a site in the destination hierarchy to own management of that content. The assigned site will access the original source file location for the content and is responsible for distributing that content to distribution points in the destination hierarchy.  

    For more information, see [Create and edit migration jobs for system center configuration manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) in [Operations for migrating to System Center Configuration Manager](../../core/migration/operations-for-migration.md).  

-   **Migrate clients to the destination hierarchy:**  

    The process of migrating clients depends on your migration scenario:  

    -   When you migrate clients that have a client version that is not the same as the destination hierarchy, you must upgrade the client software. Upgrade requires the removal of the current Configuration Manager client, followed by the installation of the new client version that matches the destination site.  

    -   When you migrate clients that have a client version that matches the version of the destination hierarchy, the client does not upgrade or reinstall. Instead, the client reassigns to a primary site in the destination hierarchy.  

    When you migrate a client to the destination hierarchy, the client is associated with its data that you previously migrated to that destination hierarchy.  

    For more information, see [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Upgrade or reassign shared distribution points:**  

    When you no longer have to support clients in your source hierarchy, you can upgrade shared distribution points from a Configuration Manager 2007 source site, or reassign shared distribution points from a System Center 2012 Configuration Manager or System Center Configuration Manager source site. When you upgrade or reassign a distribution point, the site system role transfers to a primary site in the destination hierarchy and the distribution point is removed from the source site in the source hierarchy. When you upgrade or reassign a shared distribution point, the content remains on the distribution point computer and you do not have to redeploy the content to new distribution points in the destination hierarchy.  

    You can also upgrade a distribution point that is co-located on a Configuration Manager 2007 secondary site server. This removes the secondary site and results in only a distribution point in the destination hierarchy.  

    For information about shared distribution points, see [Share distribution points between source and destination hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Finish migration:**  

    After you have migrated data and clients from all sites in the source hierarchy and you have upgraded applicable distribution points, you can finish migration. To finish migration you stop gathering data for each source site in the source hierarchy. You can then remove migration information that you do not need and decommission your source hierarchy infrastructure. For more information, see [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).  
