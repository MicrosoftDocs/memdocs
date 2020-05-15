---
title: "Custom database file locations"
titleSuffix: "Configuration Manager"
description: "Learn how to specify custom locations for SQL Server database files."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby


---
# Custom locations for Configuration Manager site database files

*Applies to: Configuration Manager (current branch)*

 Configuration Manager supports custom locations for SQL Server database files.  

> [!NOTE]  
>  The option to specify non-default file locations is not available when you use a SQL Server cluster.  

 **During setup** of a new primary site or central administration site, you can:  

-   **Specify non-default file locations for the site database**: Configuration Manager setup then creates the site database using these locations.  

-   **Specify the use of a pre-created SQL Server database that uses custom file locations**:  Configuration Manager setup then uses that pre-created database and its pre-configured file locations.  

**After setup**, you can change the location of the site database files. This requires you to stop the site and edit the file location in SQL Server:  

-   On the Configuration Manager site server, stop the **SMS_Executive** service.  

-   For more information on how to move a user database, see [Move User Databases](https://docs.microsoft.com/sql/relational-databases/databases/move-user-databases?view=sql-server-2014).  

-   After you complete the database file move, restart the **SMS_Executive** service on the Configuration Manager site server.  
