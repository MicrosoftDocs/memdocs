---
title: "About upgrade, update, and install"
titleSuffix: "Configuration Manager"
description: "Learn the difference between the terms Install, Update, and Upgrade, when managing Configuration Manager infrastructure."
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# About upgrade, update, and install for site and hierarchy infrastructure

*Applies to: System Center Configuration Manager (Current Branch)*


When managing System Center Configuration Manager site and hierarchy infrastructure, the terms *upgrade*, *update*, and *install* are used to describe three separate concepts.

## Upgrade
*Upgrade* or *in-place upgrade*, is used when converting your Configuration Manager 2012 site or hierarchy to one that runs System Center Configuration Manager.
When you upgrade System Center 2012 Configuration Manager to System Center Configuration Manager, you continue to use the same servers to host your sites and site servers, and you retain your existing data and configurations for Configuration Manager.  This is different from [Migration](/sccm/core/migration/migrate-data-between-hierarchies) which is a way to retain your configurations and data about managed devices while using new System Center Configuration Manager sites installed to new hardware.

For more details, see [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## Update
*Update* is used for installing in-console updates for System Center Configuration Manager, and for out-of-band updates which are updates that cannot be delivered from within the Configuration Manager console. In-console updates can modify the version of your Current Branch site (or Technical Preview site) so that it runs a higher version. For example, you if your site runs version 1606, you can install an update for version 1610. Updates can also install fixes for a known issue, without modifying the sites version.      

Typically, updates add security fixes, quality improvement, and new features to your existing deployment. If you use the Technical Preview branch, an update can install a newer version of the Technical Preview.
-	You choose when to install the in-console update, starting at the top-tier site of your hierarchy.
- You can install any update that is available from within the console. For example, if your site runs version 1602 and both 1606 and 1610 are offered, you should consider installing version 1610 because each version includes the features that were first made available in previously released versions.
- After a new update completes installation at your top-tier site, child primary sites automatically start the process to update. However, you can set [Service Windows](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers) to control the timing of updates.
- Secondary sites do not automatically install updates. Instead, you manually start the update from within the Configuration Manager console.

For more, see [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates), and [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## Install
*Install* is used when creating a new Configuration Manager hierarchy from scratch, or adding additional sites to an existing hierarchy.  

When you install a new primary site or central administration site, the location of setup.exe and its related source files that you use depends on your installation scenario.

For more, see [Prepare to install sites](/sccm/core/servers/deploy/install/prepare-to-install-sites).
