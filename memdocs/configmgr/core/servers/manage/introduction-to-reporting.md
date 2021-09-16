---
title: Introduction to reporting
titleSuffix: Configuration Manager
description: Learn about the set of tools and resources available to you for managing reporting in Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.localizationpriority: medium
---

# Introduction to reporting in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Reporting in Configuration Manager provides a set of tools and resources that help you use the advanced reporting capabilities of SQL Server Reporting Services (SSRS) and Power BI Report Server. Both reporting platforms provide rich authoring experiences for custom reports. Reporting helps you gather, organize, and present information about the wealth of Configuration Manager data in your organization. Configuration Manager provides many predefined reports in Reporting Services that you can use without changes. You can duplicate and modify the default reports to meet your requirements, or you can create custom reports.

## SQL Server Reporting Services

SQL Server Reporting Services provides a full range of ready-to-use tools and services to help you create, deploy, and manage reports for your organization. It also has programming features that enable you to extend and customize your reporting functionality. Reporting Services is a server-based reporting platform that provides comprehensive reporting functionality for different kinds of data sources.

Configuration Manager uses SQL Server Reporting Services as its primary reporting solution. Integration with Reporting Services provides the following advantages:  

- Uses an industry standard reporting system to query the Configuration Manager database.  

- Displays reports by using the Configuration Manager Report Viewer or by using Report Manager, which is a web-based connection to the report.  

- Provides high performance, availability, and scalability.  

- Provides subscriptions to reports to which users can subscribe. For example, a manager subscribes to an emailed report each day that details the status of a software update rollout.

- Exports reports in different kinds of popular formats.  

For more information, see [What is SQL Server Reporting Services (SSRS)?](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports)

## Power BI Report Server

<!-- 3721603 -->

Starting in version 2002, integrate Power BI Report Server with Configuration Manager reporting. This integration gives you modern visualization and better performance. It adds console support for Power BI reports similar to what already exists with SQL Server Reporting Services. For more information, see [Integrate with Power BI Report Server](powerbi-report-server.md).

Power BI Report Server is an on-premises report server with a web portal in which you display and manage reports. It includes tools to create Power BI reports, paginated reports, mobile reports, and KPIs. For more information, see [What is Power BI Report Server?](/power-bi/report-server/get-started).

## Reporting services point

The reporting services point is a site system role that you add on a server that runs Microsoft SQL Server Reporting Services. The reporting services point does the following functions:

- Copies the Configuration Manager report definitions to Reporting Services
- Creates report folders based on report categories
- Sets security policy on the report folders and reports. These policies are based on the role-based permissions for Configuration Manager administrative users. In a 10-minute interval, the reporting services point connects to Reporting Services to reapply the security policy if you changed it.

For more information about how to plan for and install a reporting services point, see the following articles:

- [Plan for reporting](planning-for-reporting.md)

- [Configure reporting](configuring-reporting.md)

## Configuration Manager reports

Configuration Manager provides report definitions for over 400 reports in over 50 report folders. During the reporting services point installation process, it copies them to the root report folder in SQL Server Reporting Services. The Configuration Manager console shows the reports and organizes them in subfolders based on the report category.

Reports don't propagate up or down the Configuration Manager hierarchy. They run only against the database of the site in which you create them. Because Configuration Manager replicates global data throughout the hierarchy, you have access to hierarchy-wide information in reports. When a report retrieves data from a site database, it has access to site data for the current site and child sites, and global data for every site in the hierarchy.

Like other Configuration Manager objects, an administrative user must have the appropriate permissions to run or modify reports. To run a report, an administrative user must have the **Run Report** permission for the object. To create or modify a report, an administrative user must have the **Modify Report** permission for the object.

### Create and modify reports

For Reporting Services-based reports, Configuration Manager uses Microsoft SQL Server Report Builder as the exclusive authoring and editing tool for model-based and SQL-based reports. When you create or edit a report in the Configuration Manager console, Report Builder opens. For more information, see [Operations and maintenance for reporting](operations-and-maintenance-for-reporting.md).

Starting in version 2002, to create or edit Power BI reports, the console integrates with Power BI Desktop. For more information, see [Create Power BI reports](powerbi-report-server.md#create-power-bi-reports).

### Run reports

When you run a Reporting Services-based report in the Configuration Manager console, Report Viewer opens and connects to Reporting Services. After you specify any required report parameters, Reporting Services then retrieves the data and displays the results in the viewer. You can also connect to the SQL Services Reporting Services, connect to the data source for the site, and run reports.

Starting in version 2002, when you run a Power BI-based report, it opens in the web browser.

### Add to Favorites

<!--8034298-->

Configuration Manager ships with several hundred reports by default, and you might add more to that list. Instead of continually searching for reports you commonly use, starting in version 2103 you can make a report a favorite. This action allows you to quickly access it from the **Favorites** node.

For more information, see [Operations and maintenance for reporting](../../servers/manage/operations-and-maintenance-for-reporting.md#favorites).

### Report prompts

You can configure a report prompt or parameter when you create or modify a report. Create report prompts to limit or target the data that a report retrieves. A report can contain more than one prompt. Make sure the prompt names are unique and contain only alphanumeric characters that conform to the SQL Server rules for identifiers.

When you run a report, the prompt requests a value for a required parameter. Based on the parameter value, it retrieves the report data. For example, the **Computer information for a specific computer** report prompts for a computer name. Reporting Services passes the specified value to a variable defined in the report's SQL statement.

### Report links

Report links in Configuration Manager are used in a source report to provide easy access to other data. For example, it can link to more detailed information about each of the items in the source report. If the destination report requires one or more prompts to run, the source report must contain a column with the appropriate values for each prompt.

The link needs to specify the column number with the value for the prompt. For example:

- There's one report that lists computers that the site recently discovered.
- You link from it to another report that lists the last messages that the site receives for a specific computer.
- You create the link, and specify that column `2` in the source report contains the computer name. This value is a required prompt for the destination report.
- You run the source report, and a link icon appears to the left of each row of data.
- You select the icon on a row, and Report Viewer passes the value in the specified column for that row as the prompt value for the destination report.

You can only configure one link for a report, and that link can only connect to a single destination report.

> [!WARNING]  
> If you move a destination report to a different report folder, the location for the destination report changes. Configuration Manager doesn't automatically update the report link in the source report with the new location, and the link won't work in the source report.

## Report folders

Report folders provide a method to sort and filter reports that Configuration Manager stores in Reporting Services. Report folders are useful when you have many reports to manage. When you install a reporting services point, it copies reports to Reporting Services and organizes them into more than 50 report folders. The report folders are read-only. You can't modify them in the Configuration Manager console.

## Report subscriptions

A report subscription in Reporting Services is a recurring request to deliver a report at a specific time or in response to an event. You specify in the subscription an application file format. Subscriptions provide an alternative to running a report on demand. On-demand reporting requires that you actively select the report each time you want to view the report. In contrast, subscriptions can be used to schedule and then automate the delivery of a report.

You can manage report subscriptions in the Configuration Manager console. The report server processes the subscriptions. It distributes them by using delivery extensions that are deployed on the server. By default, you can create subscriptions that send reports to a shared folder or to an email address.

For more information, see [Manage report subscriptions](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## Report Builder

For Reporting Services-based reports, Configuration Manager uses Microsoft SQL Server Report Builder as the exclusive authoring and editing tool for both model-based and SQL-based reports. If you create or edit a report in the Configuration Manager console, Report Builder opens. When you create or modify a report for the first time, Report Builder installs automatically. The version of Report Builder associated with the installed version of SQL Server opens when you run or edit reports.  

 The Report Builder installation adds support for over 20 languages. When you run Report Builder, it displays data in the language of the local computer's OS. If Report Builder doesn't support the language, it displays the data in English. Report Builder supports the full capabilities of SQL Server Reporting Services, which includes the following capabilities:

- Delivers an intuitive report authoring environment with an appearance similar to Microsoft 365 Apps.  

- Offers the flexible report layout of SQL Server report definition language (RDL).  

- Provides various forms of data visualization including charts and gauges.  

- Provides richly formatted text boxes.  

- Exports to Microsoft Word format.  

You can also open Report Builder directly from SQL Server Reporting Services.

## Report models in SQL Server Reporting Services

SQL Server Reporting Services uses report models to help you select items from the Configuration Manager database to include in model-based reports. When you build a report, report models expose only specified views and items to choose from. To create model-based reports, at least one report model has to be available.

Report models have the following features:

- Give logical business names to database fields and views. To produce reports, you don't require knowledge of the Configuration Manager database structure.

- Group items logically.  

- Define relationships between items.  

- Secure model elements so that administrative users can see only the data that they have permission to see.

Although Configuration Manager provides sample report models, you can also define report models to meet your own business requirements. For more information about how to create report models, see [Create custom report models](creating-custom-report-models-in-sql-server-reporting-services.md).

## Next steps

[Plan for reporting](planning-for-reporting.md)
