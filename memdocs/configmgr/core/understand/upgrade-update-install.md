---
title: About upgrade, update, and install
titleSuffix: Configuration Manager
description: Learn the difference between the terms Install, Update, and Upgrade, when managing Configuration Manager infrastructure.
ms.date: 04/30/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: concept-article
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# About upgrade, update, and install for site and hierarchy infrastructure

*Applies to: Configuration Manager (current branch)*

When managing Configuration Manager sites and hierarchy infrastructure, the terms *upgrade*, *update*, and *install* are used to describe three separate concepts.

## Upgrade

*Upgrade* or *in-place upgrade*, is used when converting your Configuration Manager 2012 site or hierarchy to one that runs Configuration Manager current branch.

When you upgrade System Center 2012 Configuration Manager to Configuration Manager current branch, you continue to use the same servers to host your sites and site servers, and you retain your existing data and configurations for Configuration Manager.  This is different from [Migration](../migration/migrate-data-between-hierarchies.md) which is a way to retain your configurations and data about managed devices while using new Configuration Manager current branch sites installed to new hardware.

For more information, see [Upgrade to Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).



## Update
*Update* is used for installing in-console updates for Configuration Manager, and for out-of-band updates which are updates that can't be delivered from within the Configuration Manager console. In-console updates can modify the version of your Current Branch site (or Technical Preview site) so that it runs a higher version. For example, if your site runs version 1806, you can install an update for version 1810. Updates can also install fixes for a known issue, without modifying the site version.      

Typically, updates add security fixes, quality improvements, and new features to your existing deployment. If you use the Technical Preview branch, an update can install a newer version of the Technical Preview.
- You choose when to install the in-console update, starting at the top-tier site of your hierarchy.
- You can install any update that is available from within the console. For example, if your site runs version 1802 and both 1806 and 1810 are offered, you should consider installing version 1810 because each version includes the features that were first made available in previously released versions.
- After a new update completes installation at your top-tier site, child primary sites automatically start the process to update. However, you can set [Service Windows](../servers/manage/service-windows.md) to control the timing of updates.
- Secondary sites don't automatically install updates. Instead, you manually start the update from within the Configuration Manager console.

For more, see [Updates for Configuration Manager](../servers/manage/updates.md), and [Technical Preview for Configuration Manager](../get-started/technical-preview.md).



## Install
*Install* is used when creating a new Configuration Manager hierarchy from scratch, or adding more sites to an existing hierarchy.  

When you install a new primary site or central administration site, the location of setup.exe and its related source files that you use depend on your installation scenario.

For more, see [Prepare to install sites](../servers/deploy/install/prepare-to-install-sites.md).
