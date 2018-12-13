---
title: "Installation scenarios"
titleSuffix: "Configuration Manager"
description: "Learn techniques for installing a new Configuration Manager hierarchy when you are updating or upgrading a site."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Scenarios to streamline your installation of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With the release of update versions for System Center Configuration Manager current branch, there are new scenarios to streamline the install of a new hierarchy to an update version (like update 1610), and to upgrade from Microsoft System Center 2012 Configuration Manager.

Supported scenarios include:  

**Install a new System Center Configuration Manager current branch hierarchy** that runs an update version.  

-   Install only the top-tier site, and then immediately install an update to bring that site current with the update version that you will use. Then, you can install additional sites directly to that update version.  
-   In this scenario, you skip the process of installing additional sites to a baseline level, and then updating them to the update version that you want to use.  
-   In this scenario, you skip the process of installing clients to a baseline version, and then reinstalling them when you update to a later version.  

**Upgrade a Microsoft System Center 2012 Configuration Manager** infrastructure to an update version of System Center Configuration Manager.  

-   Manually upgrade your central administration site and each primary site to a baseline version (like version 1606) before you install an update version (like version 1610).  
-   Don't upgrade secondary sites from Microsoft System Center 2012 Configuration Manager until your primary sites run the update version that you will use.  
-   Don't upgrade clients from Microsoft System Center 2012 Configuration Manager until your primary sites run the update version that you will use.  

## Scenario: Install a new hierarchy to an update version  
In this example scenario, install the first site of a hierarchy by using a baseline version of System Center Configuration Manager, like version 1610. Then, install the 1610 update before you deploy additional sites or clients.  

-   Because you plan to use an update version (like version 1610) and not remain at a baseline version (like version 1606), you don't need to install additional sites and then upgrade them. This also applies to clients.  
-   Don't install secondary sites with version 1606 and then upgrade them to version 1610. Instead, install secondary sites after your primary sites run version 1610.  

Follow this sequence:  

1. **Install a top-level site for your new hierarchy** by using the baseline media.  

   -   You can use baseline media only to install the first site of a new hierarchy.  
   -   For example, install a top-level site by using the baseline version of 1606. For more information, see [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

   After this step, your top-level site runs version 1606.  

2. **Use in-console updates to update your top-level site to a later version.**  

   -   Before you install any child sites or clients, update your top-level site to the update version that you plan to use.  
   -   For example, you can update your top-level site that runs version 1606 to version 1610. For more information, see [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

   After this step, your top-level site runs version 1610.  

3. **Install new child primary sites below a central administration site.**  

   - Use the installation media from the CD.Latest folder on the central administration site server to install child primary sites. For more information, see [The CD.Latest folder for System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

     This source media is required to ensure that new child primary sites match the version of the central administration site.  

   After this step, your new child primary sites run version 1610.  

4. **At each primary site, use the in-console option to install new secondary sites.**  

   -   Because you did not install secondary sites while primary sites were at version 1606, you do not need to upgrade secondary sites.  
   -   Instead, install new secondary sites that run version 1610. For more information, see [Install a secondary site](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary) in the [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites) topic.  

   After this step, new secondary sites are installed and run version 1610.  

5. **Install new clients at the primary site.**  

   -   Because you did not install clients while primary sites were at version 1606, you do not need to upgrade clients from version 1606 to version 1610.  
   -   Instead, install new clients that run version 1610. For more information, see [Deploy clients in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   After this step, new clients are installed that run version 1610.  

## Scenario: Upgrade System Center 2012 Configuration Manager to an update version of System Center Configuration Manager, current branch  
In this example scenario, upgrade your Microsoft System Center 2012 Configuration Manager infrastructure to an update version of System Center Configuration Manager, like version 1610.  

-   The central administration site and each primary site must upgrade to the baseline version 1606 before you install the update for version 1610.  
-   Secondary sites and clients do not upgrade or install version 1606. Instead, they move directly from Microsoft System Center 2012 Configuration Manager to System Center Configuration Manager version 1610.  

Follow this sequence:  

1. **Upgrade your top-level Microsoft System Center 2012 Configuration Manager site** to a baseline version of the current branch by using source media for System Center Configuration Manager (like version 1606). For more information, see [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

   -   Like traditional upgrade scenarios, you always upgrade the top-level site of a hierarchy first, and then upgrade child sites.  

   After this step, your top-level site runs version 1606.  

2. **Upgrade each child primary site in your hierarchy** to that same baseline version.  

   -   When you upgrade from Microsoft System Center 2012 Configuration Manager, you must manually upgrade each primary site to a baseline version of the current branch.  
   -   You will not upgrade secondary sites at this point.  

   After this step, each primary site runs version 1606.  

3. **Set maintenance windows on child-primary sites.** After you upgrade all your primary sites to the baseline version, plan to configure maintenance windows to control when those sites install infrastructure updates. For more information, see [How to use maintenance windows in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Maintenance windows are called *service windows* in version 1606.)  

   -   A child primary site automatically installs the same updates that you install at a central administration site.  
   -   Secondary sties do not automatically install new versions. You must upgrade them manually from within the console.  

   After this step, when you install updates at the central administration site, child primary sites will only install that update when allowed by their maintenance window.  

4. **Install the update version at your top-level site.** This updates your top-level site. After a central administration site installs the update version, each child primary site automatically installs the update unless the installation is blocked by a maintenance window.  

   -   For example, you can update your top-level site from version 1606 to version 1610. For more information, see [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

   After this step, your central administration site and each primary site runs version 1610.  

5. **Upgrade secondary sites.** After a primary site installs the update and runs version 1610, use the in-console option to upgrade secondary sites.  

   -   This upgrades secondary sites directly from Microsoft System Center 2012 Configuration Manager to the update version that you installed at the primary site.  
   -   For information about upgrading a secondary site, see [Upgrade sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) in the  [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) topic.  

6. **Upgrade clients.** To upgrade clients, use the information in [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   This upgrades clients directly from Microsoft System Center 2012 Configuration Manager to the update version that you installed at the primary site.  

   After this step, clients are upgraded to version 1610 without first upgrading to version 1606.
