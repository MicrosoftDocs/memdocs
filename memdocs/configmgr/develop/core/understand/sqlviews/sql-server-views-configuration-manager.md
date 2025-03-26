---
title: SQL Server views
titleSuffix: Configuration Manager
description: A Microsoft SQL Server view is a virtual table whose contents are based on the result from a SQL query.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms:assetid: a1924bed-b5fc-49a8-80ee-30b4e96defaa
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# SQL Server views in Configuration Manager

A Microsoft SQL Server view is a virtual table whose contents are based on the result from a SQL query. A view consists of a set of named columns and rows of data. However, the contents of a view aren't stored in the SQL Server database. The rows and columns of data come from tables or other SQL Server views referenced in the query that defines the view and are produced dynamically when the query is run. The query that defines the view can be from one or more tables or from other views in one or more databases. Distributed queries (queries that access data from multiple data sources) can also be used to define views that pull data from multiple heterogeneous sources (data stored in multiple formats), such as data stored in a SQL Server database, a text file, or a Microsoft Excel spreadsheet.

During setup, Configuration Manager creates the following SQL Server view types:

- Views against static (unchanging) tables.

- Views that use data from tables with a dynamic (changing) schema.

For a dynamic schema, setup creates a number of SQL Server stored procedures that create the views. These stored procedures are run by Configuration Manager to refresh the views when the schema of underlying tables changes. Collection evaluation, discovery, and inventory data are examples of data for which new tables or new properties in existing tables might be created during the operation of a Configuration Manager site.

## Reporting in Configuration Manager

Configuration Manager uses Microsoft SQL Server Reporting Services to allow you to generate and run reports against the Configuration Manager database, from the Configuration Manager console. This service now replaces the method used to create reports in Configuration Manager 2007, and gives the following advantages:

- Uses an industry standard reporting system to query the Configuration Manager database.

- SQL Server Reporting Services offers higher performance, availability, and scalability over the previous reporting method.

- Enables users who aren't familiar with Configuration Manager reporting to generate unplanned reports.

- Enables users to subscribe to reports; for example, a manager could automatically be e-mailed a report each day, detailing the status of a software update rollout.

- Simplifies the creation of SQL-based reports in Configuration Manager.

- Enables users to export reports in different kinds of popular formats.

For more information about using reports from the Configuration Manager console, see [Introduction to reporting](../../../../core/servers/manage/introduction-to-reporting.md).

## Configuration Manager SQL Server view schema

To create effective reports, accurate SQL statements based on the appropriate Configuration Manager views need to be used to retrieve the required data and to display the expected output. Knowing the Configuration Manager database view schema is an important first step in learning how to create these reports.

Much of the Configuration Manager SQL Server view schema maps to the SMS Provider WMI schema, which is used when building WQL-based queries and collections in the Configuration Manager console. However, querying the views directly can be much faster than using WMI and WQL, which receive a query request and in turn query the SQL Server database for the information. By using SQL Server views directly, you eliminate the intermediate step and gain a faster path to the data. For more information about the SMS Provider WMI schema, see [SMS Provider WMI Schema Reference in Configuration Manager](sms-provider-wmi-schema-reference-configuration-manager.md).

## Configuration Manager SQL Server view categories

To effectively create reports with the required output, it's essential to know what data each of the Configuration Manager SQL Server views contains and how the views are related to each other. The following topics in this section provide detailed information about each of the view categories, what kind of data each of the views contains, and what columns can be used to **JOIN** views in SQL statements.

## See also

[Create Custom Reports by Using SQL Server Views in Configuration Manager](create-custom-reports-using-sql-server-views.md)  
