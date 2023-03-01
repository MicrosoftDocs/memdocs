---
title: Reporting views
titleSuffix: Configuration Manager
description: Information about built-in and user-created reports.
ms.date: 11/22/2021
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Reporting views in Configuration Manager

Reporting in Configuration Manager uses the SQL Server Reporting Services (SSRS) to store and generate reports. For this reason, information about built-in and user-created reports is stored in the SQL Server Reporting Services database and not the Configuration Manager database.

You can run the following query against your Reporting Services database to retrieve a list of the built-in and user-created reports at your site.

```sql
    SELECT *
    FROM <report server name>.dbo.Catalog
    ORDER BY Name
```

For more information about the built-in reports supplied with Configuration Manager, see [List of reports in Configuration Manager](../../../../core/servers/manage/list-of-reports.md).

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
