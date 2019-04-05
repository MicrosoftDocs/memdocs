---
title: Creating Custom Reports by Using SQL Server Views in Configuration Manager
TOCTitle: Creating Custom Reports by Using SQL Server Views
ms:assetid: 4624ff23-d11a-4dbe-acc1-d577d13d39c7
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn581954(v=TechNet.10)
ms:contentKeyID: 60772029
ms.date: 07/27/2015
mtps_version: v=TechNet.10
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic">

<div>

# Creating Custom Reports by Using SQL Server Views in Configuration Manager

</div>

<div id="mainSection">

<div id="mainBody">

<div class="introduction">

Configuration Manager queries SQL Server views in the Configuration Manager site database to retrieve the information that is displayed in reports. The Configuration Manager site database contains a large collection of information about the network, computers, users, user groups, and many other components of the computing environment. The database also contains objects that represent Configuration Manager operations, such as deployments, software updates, configuration baselines, reports, and status messages. Configuration Manager administrators need to understand the different categories of the SQL views, what information is stored in each view, and how the SQL views can be joined to one another to create reports that return the required information. Because Configuration Manager queries and collections retrieve information from Windows Management Instrumentation (WMI) instead of Configuration Manager SQL views, it is also helpful to know how the SQL view schema is related to the WMI schema.

This documentation assumes that you have a basic understanding of Configuration Manager and SQL statements, that you have a working Configuration Manager infrastructure in place, and that you have a basic understanding of Configuration Manager reports. For more information about creating reports in Configuration Manager, see [Reporting in Configuration Manager](gg699377\(v=technet.10\).md). For more information about how to write basic SQL statements, see your SQL Server documentation.

This documentation includes an overview of the Configuration Manager SQL view schema and SQL views, an overview of the existing reports and associated reporting procedures, sample SQL statements for each Configuration Manager SQL view category, exercises for creating custom reports, an overview for writing report SQL statements, and an overview of the Configuration Manager Provider WMI schema.

</div>

<div>

## Product Versions Used in This Document

<div class="section">

This document was created using Microsoft SQL Server 2012, Report Builder 3.0 and Configuration Manager. The available SQL views, options, and commands might vary depending on the version of each product you are using. For more information, see the documentation for the products you are using.

</div>

</div>

<div>

## How to Provide Feedback about this Documentation

<div class="section">

If you have any questions or feedback about this documentation, email the [Configuration Manager Documentation Feedback Alias](mailto:smsdocs@microsoft.com).

</div>

</div>

<div>

## What’s New for Reporting in Configuration Manager

<div class="section">

This section lists the changes that have been made since Configuration Manager 2007 for Configuration Manager reporting.

</div>

<div>

## Changes made to reporting in Configuration Manager

<div class="section">

  - Configuration Manager no longer uses the reporting point; the reporting services point is the only site system role that Configuration Manager now uses for reporting.

  - Full integration of the Configuration Manager 2007 R2 SQL Server Reporting Services solution: In addition to standard report management, Configuration Manager 2007 R2 introduced support for SQL Server Reporting Services reporting. Configuration Manager integrates the Reporting Services solution, adds new functionality, and removes standard report management as a reporting solution.

  - Report Builder 2.0 integration: Configuration Manager uses Microsoft SQL Server 2008 Reporting Services Report Builder 2.0 as the exclusive authoring and editing tool for both model-based and SQL-based reports. Report Builder 2.0 is automatically installed when you create or modify a report for the first time.

  - Report subscriptions in SQL Server Reporting Services let you configure the automatic delivery of specified reports by email or to a file share in scheduled intervals.

  - You can run Configuration Manager reports in the Configuration Manager console by using Report Viewer, or you can run reports from a browser by using Report Manager. Both methods for running reports provide a similar experience.

  - Reports in Configuration Manager are rendered in the locale of the installed Configuration Manager console. Subscriptions are rendered in the locale that SQL Server Reporting Services is installed. When you author a report, you can specify the assembly and expression.

</div>

</div>

<div>

## Changes made to reporting in Configuration Manager SP1

<div class="section">

  - Configuration Manager SP1 supports Microsoft SQL Server 2012 Reporting Services.

  - When Microsoft SQL Server 2012 or SQL Server 2008 R2 runs on the Reporting Services point, Configuration Manager opens Reporting Services Report Builder 3.0 when you create or modify reports. When Microsoft SQL Server 2008 runs on the Reporting Services point, Configuration Manager opens Reporting Services Report Builder 2.0 when you create or modify reports.

  - The **Monitoring** workspace in the Configuration Manager console now displays links to SQL Server Reporting Services Report Manager from the **Reporting** node.

</div>

</div>

<div>

## Changes made to reporting in Configuration Manager

<div class="section">

  - Configuration Manager reports are now fully enabled for role-based administration. The data for all reports included with Configuration Manager is filtered based on the permissions of the administrative user who runs the report. Administrative users with specific roles can only view information defined for their roles. For more information, see the [Planning for Role-Based Administration](http://technet.microsoft.com/library/gg712693.aspx#bkmk_rolebaseadministration) for Reports section in the [Planning for Reporting in Configuration Manager](gg712693\(v=technet.10\).md) topic in the Configuration Manager Documentation Library.

</div>

</div>

</div>

<div>

## In This Section

<div class="section">

  - [SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md)  
    Provides an overview of the views you can use to create reports in Configuration Manager.

  - [Working with Reports in Configuration Manager](working-with-reports-configuration-manager.md)  
    Provides an overview of Configuration Manager reports, the elements of a report and procedures that you can use to create and manage reports.

  - [Technical Reference for SQL Server Views in Configuration Manager](technical-reference-sql-server-views-configuration-manager.md)  
    Provides sample SQL statements for each Configuration Manager SQL view category, exercises for modifying existing Configuration Manager reports and creating new reports, information about writing SQL statements and the query design tools available in SQL Server that can be used when writing report SQL statements, and an overview of the Configuration Manager WMI Provider schema.

</div>

</div>

<div>

## See Also

[Technical Publications for Configuration Manager](hh531521\(v=technet.10\).md)  

</div>

</div>

</div>

</div>

</div>

