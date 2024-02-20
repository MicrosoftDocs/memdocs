---
title: How to create a SQL statement by using query designer
titleSuffix: Configuration Manager
description: How to create Configuration Manager report queries using Query Designer.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to


ms.assetid: 2ca0c0b4-2fd1-4373-9f8d-3db7dbc92045
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# How to create a SQL statement by using query designer

Query Designer in SQL Server can help you to more easily write SQL queries that can be used in your Configuration Manager reports. Use the following procedures to create Configuration Manager report queries using Query Designer.

## To create a new SQL query in query designer

1. Start Microsoft SQL Server Management Studio.
1. Navigate to *\<Computer Name\>*�**\\ Databases \\**�*\<Configuration Manager database name\>*�**\\ Views**.
1. Right-click **Views** and then select **New View**.
1. In the **Add Table** dialog box, select the **Views** tab and then select the views that you want to include in the SQL query.

    > [!NOTE]
    > You can select multiple views by holding down the CTRL key.
1. In the design view of query designer, select the columns you want to appear in the report. If you are querying multiple views, you can join these by selecting a column in one view and dragging this over to the same column in another view.
1. Select **Execute SQL** to test the query and see the results.
1. When you are happy with the results returned by the query, copy and paste it from query designer to be used to create your report in Report Builder.

## See also

[SQL statement reference for Configuration Manager reports](sql-statement-reference-configuration-manager-reports.md)
