---
title: SQL Server Views in Configuration Manager
TOCTitle: SQL Server Views in Configuration Manager
ms:assetid: 9e955713-be09-4769-9c61-e741fdbf4d12
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn581978(v=TechNet.10)
ms:contentKeyID: 60772078
ms.prod: "configuration-manager"
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2019
mtps_version: v=TechNet.10
---

# SQL Server Views in Configuration Manager

A Microsoft SQL Server view is a virtual table whose contents are based on the result from a SQL query. A view consists of a set of named columns and rows of data. However, the contents of a view are not stored in the SQL database. The rows and columns of data come from tables or other SQL views referenced in the query that defines the view and are produced dynamically when the query is run. The query that defines the view can be from one or more tables or from other views in one or more databases. Distributed queries (queries that access data from multiple data sources) can also be used to define views that pull data from multiple heterogeneous sources (data stored in multiple formats), such as data stored in a SQL Server database, a text file, or a Microsoft Excel spreadsheet.

During setup, Configuration Manager creates the following SQL view types:

- Views against static (unchanging) tables.

- Views that use data from tables with a dynamic (changing) schema.

For a dynamic schema, setup creates a number of SQL Server stored procedures that create the views. These stored procedures are run by Configuration Manager to refresh the views when the schema of underlying tables changes. Collection evaluation, discovery, and inventory data are examples of data for which new tables or new properties in existing tables might be created during the operation of a Configuration Manager site.

## Reporting in Configuration Manager

Configuration Manager uses Microsoft SQL Server Reporting Services to allow you to generate and run reports against the Configuration Manager database, from the Configuration Manager console. This now replaces the method used to create reports in Configuration Manager 2007. This gives the following advantages:

- Uses an industry standard reporting system to query the Configuration Manager database.

- SQL Reporting Services offers higher performance, availability and scalability over the previous reporting method.

- Enables users who are not familiar with Configuration Manager reporting to generate ad hoc reports.

- Enables users to subscribe to reports; for example, a manager could automatically be e-mailed a report each day, detailing the status of a software update rollout.

- Simplifies the creation of SQL-based reports in Configuration Manager.

- Enables users to export reports in a variety of popular formats.

For more information about using reports from the Configuration Manager console, see [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting).

## Configuration Manager SQL View Schema

To create effective reports, accurate SQL statements based on the appropriate Configuration Manager views need to be used to retrieve the required data and to display the expected output. Knowing the Configuration Manager database view schema is an important first step in learning how to create these reports.

Much of the Configuration Manager SQL view schema maps to the SMS Provider WMI schema, which is used when building WQL-based queries and collections in the Configuration Manager console. However, querying the views directly can be much faster than using WMI and WQL, which receive a query request and in turn query the SQL database for the information. By using SQL views directly, you eliminate the intermediate step and gain a faster path to the data. For more information about the SMS Provider WMI schema, see [SMS Provider WMI Schema Reference in Configuration Manager](sms-provider-wmi-schema-reference-configuration-manager.md).

## Configuration Manager SQL View Categories

To effectively create reports with the required output, it is essential to know what data each of the Configuration Manager SQL Server views contains and how the views are related to each other. The following topics in this section provide detailed information about each of the view categories, what kind of data each of the views contains, and what columns can be used to **JOIN** views in SQL statements.

## See Also

[Creating Custom Reports by Using SQL Server Views in Configuration Manager](creating-custom-reports-using-sql-server-views.md)  
