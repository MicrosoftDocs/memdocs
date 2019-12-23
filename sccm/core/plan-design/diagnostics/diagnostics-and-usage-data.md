---
title: Diagnostics and usage data
titleSuffix: Configuration Manager
description: Learn about the diagnostics and usage data that Configuration Manager collects about itself.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Diagnostics and usage data for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager collects diagnostics and usage data about itself, which is used by Microsoft to improve the installation experience, quality, and security of future releases.  

Each Configuration Manager hierarchy enables diagnostics and usage data. It consists of SQL Server queries that run on a weekly basis on each primary site and at the central administration site (CAS). When the hierarchy uses a CAS, child primary sites replicate their data to that CAS. At the top-level site of your hierarchy, the [service connection point](/configmgr/core/servers/deploy/configure/about-the-service-connection-point) submits this information when it checks for updates. If the service connection point is in offline mode, you transfer the information by using the [service connection tool](/configmgr/core/servers/manage/use-the-service-connection-tool).

> [!NOTE]  
> Configuration Manager collects data only from the site's SQL server database, and it doesn't collect data directly from clients or site servers.  

For more information, see the [Microsoft privacy statement](https://go.microsoft.com/fwlink/?LinkID=626527).  

> [!div class="nextstepaction"]
> [How Configuration Manager collects data](/configmgr/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)
