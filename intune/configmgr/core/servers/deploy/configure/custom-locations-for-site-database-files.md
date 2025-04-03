---
title: Custom database file locations
titleSuffix: Configuration Manager
description: Learn how to specify custom locations for SQL Server database files.
ms.date: 10/08/2020
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Custom locations for Configuration Manager site database files

*Applies to: Configuration Manager (current branch)*

Configuration Manager supports custom locations for SQL Server database files.

> [!NOTE]
> The option to specify non-default file locations isn't available when you use a SQL Server Always On failover cluster instance.

During setup of a new primary site or central administration site, you can:

- **Specify non-default file locations for the site database**: Configuration Manager setup then creates the site database using these locations.

- **Specify the use of a pre-created SQL Server database that uses custom file locations**: Configuration Manager setup then uses that pre-created database and its pre-configured file locations.

After setup, you can change the location of the site database files. This requires you to stop the site and edit the file location in SQL Server:

1. On the Configuration Manager site server, stop the **SMS_Executive** service.

1. Move the database in SQL Server. For more information, see [Move User Databases](/sql/relational-databases/databases/move-user-databases).

1. After you complete the database file move, restart the **SMS_Executive** service on the Configuration Manager site server.
