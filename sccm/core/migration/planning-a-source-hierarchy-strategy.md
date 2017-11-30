---
title: "Source hierarchy strategy"
titleSuffix: "Configuration Manager"
description: "Configure a source hierarchy and gather data from a source site before you configure a System Center Configuration Manager migration job."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
caps.latest.revision: 6
caps.handback.revision: 0
author: aaroncz
ms.author: aaroncz
manager: angrobe

---
# Plan a source hierarchy strategy in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you set up a migration job in your System Center Configuration Manager environment, you must configure a source hierarchy and gather data from at least one source site in that hierarchy. Use the following sections to help you plan for configuring source hierarchies, configuring source sites, and determining how Configuration Manager gathers information from the source sites in the source hierarchy. 

##  <a name="BKMK_Source_Hierarchies"></a> Source hierarchies  
A source hierarchy is a Configuration Manager hierarchy that has data that you want to migrate. When you set up migration and specify a source hierarchy, you specify the top-level site of the source hierarchy. This site is also called a source site. Additional sites that you can migrate data from in the source hierarchy are also called source sites.  

-   When you set up a migration job to migrate data from a Configuration Manager 2007 source hierarchy, you configure it to migrate data from one or more specific source sites in the source hierarchy.  

-   When you set up a migration job to migrate data from a source hierarchy that runs System Center 2012 Configuration Manager or later, you only need to specify the top-level site.  

You can set up only one source hierarchy at a time.  

-   If you set up a new source hierarchy, that hierarchy automatically becomes the current source hierarchy replacing the previous source hierarchy.  

-   When you set up a source hierarchy, you must specify the top-level site of the source hierarchy and specify credentials for Configuration Manager to use to connect to the SMS Provider and site database of that source site.  

-   Configuration Manager uses these credentials to run data gathering to retrieve information about the objects and distribution points from the source site.  

-   As part of the data gathering process, child sites in the source hierarchy are identified.  

-   If the source hierarchy is a Configuration Manager 2007 hierarchy, you can set up those additional sites as source sites with separate credentials for each source site.  

Although you can set up multiple source hierarchies in succession, migration is active for only one source hierarchy at a time.  

-   If you set up an additional source hierarchy before you complete migration from the current source hierarchy, Configuration Manager cancels any active migration jobs and postpones any scheduled migration jobs for the current source hierarchy.  

-   The newly configured source hierarchy then becomes the current source hierarchy, and the original source hierarchy is now inactive.  

-   You can then set up connection credentials, additional source sites, and migration jobs for the new source hierarchy.  

If you restore an inactive source hierarchy and have not previously used **Cleanup Migration Data**, you can view the previously configured migration jobs for that source hierarchy. However, before you can continue migration from that hierarchy, you must reconfigure the credentials to connect to applicable source sites in the hierarchy, and then reschedule any migration jobs that did not finish.  

> [!CAUTION]  
>  If you migrate data from more than a single source hierarchy, each additional source hierarchy must contain a unique set of site codes.  

For more about configuring a source hierarchy, see [Configuring source hierarchies and source sites for migration to System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="BKMK_Source_Sites"></a> Source sites  
 Source sites are the sites in the source hierarchy that have the data that you want to migrate. The top-level site of the source hierarchy is always the first source site. When migration collects data from the first source site of a new source hierarchy, it discovers information about additional sites in that hierarchy.  

 After data gathering completes for the initial source site, the actions you take next depend on the product version of the source hierarchy.  

### Source sites that run Configuration Manager 2007 SP2  
 After data is gathered from the initial source site of the Configuration Manager 2007 SP2 hierarchy, you do not have to set up additional source sites before you create migration jobs. However, before you can migrate data from additional sites, you must set up additional sites as source sites, and System Center Configuration Manager must successfully gather data from those sites.  

 To gather data from additional sites, you individually set up each site as a source site. This requires you to specify the credentials for System Center Configuration Manager to connect to the SMS Provider and site database of each source site. After you set up the credentials for a source site, the data gathering process for that site begins.  

 When you set up additional source sites in a Configuration Manager 2007 SP2 source hierarchy, you must set up source sites from the top down, which means you set up the bottom-tier sites last. You can configure source sites in a branch of the hierarchy at any time, but you must set up a site as a source site before you set up any of its child sites as source sites.  

> [!NOTE]  
>  Only primary sites in a Configuration Manager 2007 SP2 hierarchy are supported for migration.  

### Source sites that run System Center 2012 Configuration Manager or later  
 After data is gathered from the initial source site of the System Center 2012 Configuration Manager or later hierarchy, you do not have to set up additional source sites in that source hierarchy. This is because unlike Configuration Manager 2007, these versions of Configuration Manager use a shared database, and the shared database lets you identify and then migrate all available objects from the initial source site.  

 When you set up the access accounts to gather data, you might need to grant the **Source Site SMS Provider Account** access to multiple computers in the source hierarchy. This might be needed when the source site supports multiple instances of the SMS Provider, each on a different computer. When data gathering begins, the top-level site of the destination hierarchy contacts the top-level site in the source hierarchy to identify the locations of the SMS Provider for that site. Only the first instance of the SMS provider is identified. If the data gathering process cannot access the SMS Provider at the location it identifies, the process fails and does not try to connect to additional computers that run an instance of SMS Provider for that site.  

##  <a name="BKMK_Data_Gathering"></a> Data gathering  
 Immediately after you specify a source hierarchy, set up credentials for each additional source site in a source hierarchy, or share the distribution points for a source site, Configuration Manager starts to gather data from the source site.  

 The data gathering process then repeats itself on a simple schedule to maintain synchronization with any changes to data in the source site. By default, the process repeats every four hours. You can change the schedule for this cycle by editing the **Properties** of the source site. The initial data gathering process must review all objects in the Configuration Manager database and can take a long time to finish. Subsequent data gathering processes identify only changes to the data and require less time to finish.  

 To gather data, the top-level site in the destination hierarchy connects to the SMS Provider and the site database of the source site to retrieve a list of objects and distribution points. These connections use the source site access accounts. For information about required configurations for gathering data, see [Prerequisites for migration in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 You can start and stop the data gathering process by using **Gather Data Now** and **Stop Gathering Data** in the Configuration Manager console.  

 After you use **Stop Gathering Data** for a source site for any reason, you must reconfigure credentials for the site before you can gather data from that site again. Until you reconfigure the source site, Configuration Manager cannot identify new objects or changes to previously migrated objects at that site.  

> [!NOTE]  
>  Before you expand a standalone primary site into a hierarchy with a central administration site, you must stop all data gathering. You can reconfigure data gathering after the site expansion completes.  

### Gather Data Now  
 After the initial data gathering process runs for a site, this process repeats itself to identify objects that have updated since the last data gathering cycle. You can also use the **Gather Data Now** action in the Configuration Manager console to immediately start the process and to reset the start time of the next cycle.  

 After a data gathering process successfully finishes for a source site, you can share the distribution points from the source site and configure migration jobs to migrate data from the site. Data gathering is a repeating process for migration, and it continues until you change the source hierarchy or use **Stop Gathering Data** to end the data gathering process for that site.  

### Stop Gathering Data  
 You can use **Stop Gathering Data** to end the data gathering process for a source site when you no longer want Configuration Manager to identify new or changed objects from that site. This action also prevents Configuration Manager from offering clients in the destination hierarchy any shared distribution points from the source as content locations for the content that you have migrated.  

 To stop gathering data from each source site, you must run **Stop Gathering Data** on the bottom-tier source sites, and then repeat the process at each parent site. The top-level site of the source hierarchy must be the last site on which you stop gathering data. You must stop data gathering at each child site before performing this action at a parent site. Typically, you only stop gathering data when you are ready to complete the migration process.  

 After you stop gathering data for a source site, information previously gathered about objects and collections from that site remain available to use when you set up new migration jobs. However, you do not see any new objects or collections, nor do you see changes that were made to existing objects. If you reconfigure the source site and begin gathering data again, you will see information and status about previously migrated objects.  
