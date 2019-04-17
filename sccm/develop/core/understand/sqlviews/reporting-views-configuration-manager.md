---
title: Reporting Views
titleSuffix: Configuration Manager
description: Information about built-in and user-created reports.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 6a557d1e-fcf3-4b3f-b514-2f335ac4d14e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Reporting Views in Configuration Manager

Reporting in Configuration Manager uses the SQL Reporting Services (SSRS) to store and generate reports. For this reason, information about built-in and user-created reports is stored in the SQL Reporting Services database and not the Configuration Manager database.

You can run the following query against your Reporting Services database to retrieve a list of the built-in and user-created reports at your site.

    SELECT *
    FROM <report server name>.dbo.Catalog
    ORDER BY Name

For more information about the built-in reports supplied with Configuration Manager, see [List of Reports Supplied with Configuration Manager](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/dn581998(v=technet.10)).

## See Also

[SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md)  