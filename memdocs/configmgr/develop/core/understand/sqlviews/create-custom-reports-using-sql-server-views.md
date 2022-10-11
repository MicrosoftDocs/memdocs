---
title: Creating custom reports by using SQL Server views
titleSuffix: Configuration Manager
description: Information about how to create reports directly from the Configuration Manager console.
ms.date: 06/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms: "assetid: 5741ada8-449c-45af-85e1-2e68abf96440"
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Creating custom reports by using SQL Server views in Configuration Manager

Configuration Manager queries SQL Server views in the Configuration Manager site database to retrieve the information that is displayed in reports. The Configuration Manager site database contains a large collection of information about the network, computers, users, user groups, and many other components of the computing environment. The database also contains objects that represent Configuration Manager operations, such as deployments, software updates, configuration baselines, reports, and status messages. Configuration Manager administrators need to understand the different categories of the SQL views, what information is stored in each view, and how the SQL views can be joined to one another to create reports that return the required information. Because Configuration Manager queries and collections retrieve information from Windows Management Instrumentation (WMI) instead of Configuration Manager SQL views, it is also helpful to know how the SQL view schema is related to the WMI schema.

This documentation assumes that you have a basic understanding of Configuration Manager and SQL statements, that you have a working Configuration Manager infrastructure in place, and that you have a basic understanding of Configuration Manager reports. For more information about creating reports in Configuration Manager, see [Introduction to reporting](../../../../core/servers/manage/introduction-to-reporting.md). For more information about how to write basic SQL statements, see your SQL Server documentation.

This documentation includes an overview of the Configuration Manager SQL view schema and SQL views, an overview of the existing reports and associated reporting procedures, sample SQL statements for each Configuration Manager SQL view category, exercises for creating custom reports, an overview for writing report SQL statements, and an overview of the Configuration Manager Provider WMI schema.

## Product versions used in this document

This document was created using Microsoft SQL Server 2012, Report Builder 3.0 and Configuration Manager. The available SQL views, options, and commands might vary depending on the version of each product you are using. For more information, see the documentation for the products you are using.

## What's new for reporting in Configuration Manager

This section lists the changes that have been made since Configuration Manager 2007 for Configuration Manager reporting.

- Configuration Manager no longer uses the reporting point; the reporting services point is the only site system role that Configuration Manager now uses for reporting.

- Full integration of the Configuration Manager 2007 R2 SQL Server Reporting Services solution: In addition to standard report management, Configuration Manager 2007 R2 introduced support for SQL Server Reporting Services reporting. Configuration Manager integrates the Reporting Services solution, adds new functionality, and removes standard report management as a reporting solution.

- Report Builder 2.0 integration: Configuration Manager uses Microsoft SQL Server 2008 Reporting Services Report Builder 2.0 as the exclusive authoring and editing tool for both model-based and SQL-based reports. Report Builder 2.0 is automatically installed when you create or modify a report for the first time.

- Report subscriptions in SQL Server Reporting Services let you configure the automatic delivery of specified reports by email or to a file share in scheduled intervals.

- You can run Configuration Manager reports in the Configuration Manager console by using Report Viewer, or you can run reports from a browser by using Report Manager. Both methods for running reports provide a similar experience.

- Reports in Configuration Manager are rendered in the locale of the installed Configuration Manager console. Subscriptions are rendered in the locale that SQL Server Reporting Services is installed. When you author a report, you can specify the assembly and expression.

- When Microsoft SQL Server 2012 or SQL Server 2008 R2 runs on the Reporting Services point, Configuration Manager opens Reporting Services Report Builder 3.0 when you create or modify reports. When Microsoft SQL Server 2008 runs on the Reporting Services point, Configuration Manager opens Reporting Services Report Builder 2.0 when you create or modify reports.

- The **Monitoring** workspace in the Configuration Manager console now displays links to SQL Server Reporting Services Report Manager from the **Reporting** node.

- Configuration Manager reports are now fully enabled for role-based administration. The data for all reports included with Configuration Manager is filtered based on the permissions of the administrative user who runs the report. Administrative users with specific roles can only view information defined for their roles. For more information, see the [Planning for Role-Based Administration](../../../../core/servers/manage/planning-for-reporting.md#plan-for-role-based-administration) for Reports section in the  Planning for Reporting in Configuration Manager article in the Configuration Manager Documentation Library.

## In this section

- **SQL Server views in Configuration Manager**  
  Provides an overview of the views you can use to create reports in Configuration Manager.

- **Working with reports in Configuration Manager**  
  Provides an overview of Configuration Manager reports, the elements of a report and procedures that you can use to create and manage reports.

- **Technical reference for SQL Server views in Configuration Manager**  
  Provides sample SQL statements for each Configuration Manager SQL view category, exercises for modifying existing Configuration Manager reports and creating new reports, information about writing SQL statements and the query design tools available in SQL Server that can be used when writing report SQL statements, and an overview of the Configuration Manager WMI Provider schema.

## See also

- [Exploring your Configuration Manager data on Power BI dashboard](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Exploring-your-System-Center-Configuration-Manager-and-Microsoft/ba-p/273970)
