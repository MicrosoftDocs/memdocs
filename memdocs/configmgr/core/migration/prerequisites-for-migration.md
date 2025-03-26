---
title: Migration prerequisites
titleSuffix: Configuration Manager
description: Understand the supported versions of Configuration Manager, supported source-site languages, and required configurations for migration.
ms.date: 05/7/2018
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

# Prerequisites for migration in Configuration Manager

*Applies to: Configuration Manager (current branch)*

To migrate from a supported source hierarchy, you must have access to each applicable Configuration Manager source site, and permissions within the Configuration Manager destination site to configure and run migration operations.  

 Use the information in the following sections to help you understand the versions of Configuration Manager that are supported for migration, and the required configurations.  

-   [Versions of Configuration Manager that are supported for migration](#BKMK_SupportedMigrationVersions)  

-   [Source site languages that are supported for migration](#BKMK_SorceSiteLanguage)  

-   [Required configurations for migration](#BKMK_Required_Configurations)  

##  <a name="BKMK_SupportedMigrationVersions"></a> Versions of Configuration Manager that are supported for migration  
 You can migrate data from a source hierarchy that runs any of  the following versions of Configuration Manager:  

- Configuration Manager 2007 SP2  (For the purpose of migration, Configuration Manager 2007 R2 or R3 on the source site are not a consideration. So long as the source site runs SP2, sites with either the R2 or R3  add-on installed are supported for migration to Configuration Manager current branch).  

- System Center 2012 Configuration Manager SP2 or System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  In addition to migration, you can use an in-place upgrade of sites that run System Center 2012 Configuration Manager to Configuration Manager current branch.  

- A Configuration Manager hierarchy of the same or lesser version of Configuration Manager.  

  For example, if you have a destination hierarchy that runs Configuration Manager current branch 1606, you could use migration to copy data from a source hierarchy that runs version 1606 or 1602. However you could not migrate data from a source hierarchy that runs 1610.  


##  <a name="BKMK_SorceSiteLanguage"></a> Source site languages that are supported for migration  
 When you migrate data between Configuration Manager hierarchies, the data is stored in the destination hierarchy in the language neutral format for Configuration Manager. Because Configuration Manager 2007 does not store data in a language neutral format, the migration process must convert objects to this format during migration from Configuration Manager 2007. Therefore, only Configuration Manager 2007 source sites that are installed with the following languages are supported for migration:  

-   English  

-   French  

-   German  

-   Japanese  

-   Korean  

-   Russian  

-   Simplified Chinese  

-   Traditional Chinese  

When you migrate data from a System Center 2012 Configuration Manager or Configuration Manager current branch hierarchy, there are no source site language limitations. Objects in the source site database are already in a language neutral format.  

##  <a name="BKMK_Required_Configurations"></a> Required configurations for migration  
The following are required configurations for using migration and migration operations:  

- **To configure, run, and monitor migration in the Configuration Manager console:**  

   In the destination site, your account must be assigned the role-based administration security role of **Infrastructure Administrator**. This security role grants permissions to manage all migration operations, which includes the creation of migration jobs, clean up, monitoring, and the action to share and upgrade distribution points.  

- **Data Gathering:**  

   To enable the destination site to gather data, you must configure the following two source site access accounts for use with each source site:  

  -   **Source Site Account:** This account is used to access the SMS Provider of the source site.  

      -   For a Configuration Manager 2007 SP2 source site, this account requires **Read** permission to all source site objects.  

      -   For a System Center 2012 Configuration Manager or Configuration Manager current branch source site, this account requires **Read** permission to all source site objects, You grant this permission to the account by using role-based administration. For information about how to use role-based administration, see [Fundamentals of role-based administration for Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

  -   **Source Site Database Account:** This account is used to access the SQL Server database of the source site and requires **Connect**, **Execute**, and **Select** permissions to the source site database.  

  You can configure these accounts when you configure a new source hierarchy, data gathering for an additional source site, or when you reconfigure the credentials for a source site. These accounts can use a domain user account, or you can specify the computer account of the top-level site of the destination hierarchy.  

  > [!IMPORTANT]  
  >  If you use the Configuration Manager computer account for either access account, ensure that this account is a member of the security group **Distributed COM Users** in the domain where the source site resides.  

  When gathering data, the following network protocols and ports are used:  

  - NetBIOS/SMB - 445 (TCP)  

  - RPC (WMI) - 135 (TCP & UDP)  

  - Dynamic RPC. Dynamic ports use a range of port numbers that are defined by the OS version. These ports are also known as ephemeral ports. For more information about the default port ranges, see [Service overview and network port requirements for Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).<!-- SCCMDocs#1053 -->

  - SQL Server - The TCP ports in use by both the source and destination site databases.  

- **Migrate Software Updates:**  

   Before you migrate software updates, you must configure the destination hierarchy with a software update point. For more information, see [Planning to migrate software updates](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Share distribution points:**  

   To successfully share any distribution points from a source site, at least one primary site or the central administration site in the destination hierarchy must use the same port numbers for client requests as the source site. For information about client request ports, see [How to configure client communication ports](../../core/clients/deploy/configure-client-communication-ports.md)  

   For each source site, only the distribution points that are installed on site system servers that are configured with a FQDN are shared.  

   In addition, to share a distribution point from a System Center 2012 Configuration Manager or Configuration Manager current branch source site, the **Source Site Account** (which accesses the SMS Provider for the source site server), must have **Modify** permissions to the **Site** object on the source site. You grant this permission to the account by using role-based administration. For information about how to use role-based administration, see [Fundamentals of role-based administration for Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


- **Upgrade or reassign distribution points:**  

   The **Source Site Access Account** configured to gather data from the SMS Provider of the source site must have the following permissions:  

  - To upgrade a Configuration Manager 2007 distribution point, the account requires **Read**, **Execute**, and **Delete** permissions to the **Site** class on the Configuration Manager2007 site server to successfully remove the distribution point from the Configuration Manager2007 source site  

  - To reassign a System Center 2012 Configuration Manager or Configuration Manager current branch distribution point, the account must have **Modify** permission to the **Site** object on the source site. You grant this permission to the account by using role-based administration. For information about how to use role-based administration, see [Fundamentals of role-based administration for Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    To successfully upgrade or reassign a distribution point to a new hierarchy, the ports that are configured for client requests at the site that manages the distribution point in the source hierarchy must match the ports that are configured for client requests at the destination site that will manage the distribution point. For information about client request ports, see [How to configure client communication ports](../../core/clients/deploy/configure-client-communication-ports.md).  
