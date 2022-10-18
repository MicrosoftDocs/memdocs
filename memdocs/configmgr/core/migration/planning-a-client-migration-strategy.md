---
title: Plan client migration
titleSuffix: Configuration Manager
description: Learn about the tasks that migrate clients from a source hierarchy to a Configuration Manager current branch destination hierarchy.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Plan a client migration strategy in Configuration Manager

*Applies to: Configuration Manager (current branch)*

To migrate clients from the source hierarchy to a Configuration Manager current branch destination hierarchy, you must do two tasks. You must migrate the objects that are associated with the client and you must then reinstall or reassign the clients from the source hierarchy to the destination hierarchy. You migrate the objects first so that they are available when the clients are migrated. The objects associated with the client are migrated by using migration jobs. For information about how to migrate the objects that are associated with the client, see [Planning a migration job strategy](../../core/migration/planning-a-migration-job-strategy.md).  

 Use the following sections to help you plan to migrate clients to the destination hierarchy.  

-   [Plan to migrate clients to the destination hierarchy](#Planning_for_Client_Agent_Migration)  

-   [Plan to handle data maintained on clients during migration](#Planning_for_Client_Data_Migration)  

-   [Plan for inventory and compliance data during migration](#Planning_for_Inventory_data_migration)  

##  <a name="Planning_for_Client_Agent_Migration"></a> Plan to migrate clients to the destination hierarchy  
 When you migrate clients from a source hierarchy, the client software on the client computer upgrades to match the product version of the destination hierarchy.  

-   **A Configuration Manager 2007 source hierarchy:** When you migrate clients from a source hierarchy that runs a supported version of Configuration Manager, the client software upgrades to the client version for the destination hierarchy.  

-   **A System Center 2012 Configuration Manager or later source hierarchy:** When you migrate clients between hierarchies that are of the same product version, the client software does not change or upgrade. Instead, the client reassigns from the source hierarchy to a site in the destination hierarchy.  

    > [!NOTE]  
    >  When the product version of a hierarchy is not supported for migration to your destination hierarchy, upgrade all sites and clients in the source hierarchy to a compatible product version. After the source hierarchy upgrades to a supported product version, you can migrate between the hierarchies. For more information, see [Versions of Configuration Manager that are supported for migration](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) in [Prerequisites for migration](../../core/migration/prerequisites-for-migration.md).  

Use the following information to help you plan the client migration:  

-   To upgrade or reassign clients from a source site to a destination site, you can use any client deployment method that is supported for deploying clients in the destination hierarchy. Typical client deployment methods include client push installation, software distribution, Group Policy, and software update-based client installation. For more information, see [Client installation methods](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Ensure that the device that runs the client software in the source hierarchy meets the minimum hardware requirements and runs an operating system that is supported by the version of Configuration Manager in the destination hierarchy.  

-   Before you migrate a client, run a migration job to migrate the information that the client will use in the destination hierarchy.  

-   Clients that upgrade retain their run history for deployments. This prevents deployments from rerunning unnecessarily in the destination hierarchy.  

    -   For Configuration Manager 2007 clients, advertisement run history is retained.  

    -   For clients from System Center 2012 Configuration Manager or Configuration Manager current branch, deployment run history is retained.  

-   You can migrate clients from sites in the source hierarchy in any order that you choose. However, consider migrating limited numbers of clients in phases rather than migrating large numbers of clients at a single time. A phased migration reduces the network bandwidth requirements and server processing when each newly upgraded client submits its initial full inventory and compliance data to its assigned site.  

-   When you migrate Configuration Manager 2007 clients, the existing client software is uninstalled from the client computer and the new client software is installed.  

-   Configuration Manager cannot migrate a Configuration Manager 2007 client that has the App-V client installed unless the App-V client version is 4.6 SP1 or later.  

You can monitor the client migration process in the **Migration** node of the **Administration** workspace in the Configuration Manager console.  

After you migrate the client to the destination hierarchy, you can no longer manage that device by using your source hierarchy, and you should consider removing the client from the source hierarchy. Although this is not a requirement when you migrate hierarchies, it can help prevent identification of a migrated client in a source hierarchy report, or an incorrect count of resources between the two hierarchies during the migration. For example, when a migrated client remains in the source site database, you might run a software updates report that incorrectly identifies the computer as an unmanaged resource when it is now managed by the destination hierarchy.  

##  <a name="Planning_for_Client_Data_Migration"></a> Plan to handle data maintained on clients during migration  
When you migrate a client from its source hierarchy to the destination hierarchy, some information is retained on the device, while other information is not available on the device after migration.  

The following information is retained on the client device:  

-   The unique identifier (GUID), which associates a client with its information in the Configuration Manager database.  

-   The advertisement or deployment history, which prevents clients from unnecessarily rerunning advertisements or deployments in the destination hierarchy.  

The following information is not retained on the client device:  

-   The files in the client cache. If the client requires these files to install software, the client downloads them again from the destination hierarchy.  

-   Information from the source hierarchy about any advertisements or deployments that have not yet run. If you want the client to run the advertisements or deployments after it migrates, you must redeploy them to the client in the destination hierarchy.  

-   Information about inventory. The client resends this information to its assigned site in the destination hierarchy after the client migrates and the new client data has been generated.  

-   Compliance data. The client resends this information to its assigned site in the destination hierarchy after the client migrates and the new client data has been generated.  

When a client migrates, information that is stored in the Configuration Manager client registry and file path is not retained. After migration, reapply these settings. Typical settings include the following:  

-   Power schemes  

-   Logging settings  

-   Local policy settings  

Additionally, you might have to reinstall some applications.  

##  <a name="Planning_for_Inventory_data_migration"></a> Plan for  inventory and compliance data during migration  
Client inventory and compliance data is not saved when you migrate a client to the destination hierarchy. Instead, this information is recreated in the destination hierarchy when a client first sends its information to its assigned site. To help reduce the resulting network bandwidth requirements and server processing, consider migrating a small number of clients in phases rather than migrating a large number of clients at a single time.  

 Additionally, you cannot migrate customizations for hardware inventory from a source hierarchy. You must introduce these to the destination hierarchy independently from migration. For information about how to extend hardware inventory, see [How to configure hardware inventory](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
