---
title: Introduction to reporting 
titleSuffix: "Configuration Manager"
description: "Learn about the set of tools and resources available to you for managing reporting in Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
caps.latest.revision: 7
author: Dougebyms.author: dougebymanager: angrobe

---
# Introduction to reporting in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Reporting in System Center Configuration Manager provides a set of tools and resources that help you use the advanced reporting capabilities of SQL Server Reporting Services (SSRS) and the rich authoring experience that Reporting Services Report Builder provides. Reporting helps you gather, organize, and present information about users, hardware and software inventory, software updates, applications, site status, and other Configuration Manager operations in your organization. Reporting provides you with a number of predefined reports that you can use without changes, or that you can modify to meet your requirements, and you can create custom reports. Use the following sections to help you manage reporting in Configuration Manager.  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services provides a full range of ready-to-use tools and services to help you create, deploy, and manage reports for your organization and programming features that enable you to extend and customize your reporting functionality. Reporting Services is a server-based reporting platform that provides comprehensive reporting functionality for a variety of data sources.  

 Configuration Manager uses SQL Server Reporting Services as its reporting solution. Integration with Reporting Services provides the following advantages:  

-   Uses an industry standard reporting system to query the Configuration Manager database.  

-   Displays reports by using the Configuration Manager Report Viewer or by using Report Manager, which is a web-based connection to the report.  

-   Provides high performance, availability, and scalability.  

-   Provides subscriptions to reports that users can subscribe to; for example, a manager could subscribe to automatically receive an emailed report each day that details the status of a software update rollout.  

-   Exports reports that users can select in a variety of popular formats.  

 For more information about Reporting Services, see [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) in the SQL Server 2008 Books Online.  

##  <a name="BKMK_ReportingServicesPoint"></a> Reporting Services Point  
 The reporting services point is a site system role that is installed on a server that is running Microsoft SQL Server Reporting Services. The reporting services point copies the Configuration Manager report definitions to Reporting Services, creates report folders based on report categories, and sets security policy on the report folders and reports based on the role-based permissions for Configuration Manager administrative users. In a 10-minute interval, the reporting services point connects to Reporting Services to reapply the security policy if it has been changed, for example, by using Report Manager. For more information about how to plan for and install a reporting services point, see the following documentation:  

-   [Planning for reporting in System Center Configuration Manager](planning-for-reporting.md)  

-   [Configuring reporting in System Center Configuration Manager](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Configuration Manager reports  
 Configuration Manager provides report definitions for over 400 reports in over 50 report folders, which are copied to the root report folder in SQL Server Reporting Services during the reporting services point installation process. The reports are displayed in the Configuration Manager console and organized in subfolders based on the report category. Reports are not propagated up or down the Configuration Manager hierarchy; they run only against the database of the site in which they are created. However, because Configuration Manager replicates global data throughout the hierarchy, you have access to hierarchy-wide information. When a report retrieves data from a site database, it has access to site data for the current site and child sites, and global data for every site in the hierarchy. Like other Configuration Manager objects, an administrative user must have the appropriate permissions to run or modify reports. To run a report, an administrative user must have the **Run Report** permission for the object. To create or modify a report, an administrative user must have the **Modify Report** permission for the object.  

###  <a name="BKMK_CreatingReports"></a> Creating and modifying reports  
 Configuration Manager uses Microsoft SQL Server Report Builder as the exclusive authoring and editing tool for model-based and SQL-based reports. When you create or edit a report in the Configuration Manager console, Report Builder opens. For more information about managing reports, see the [Operations and maintenance for reporting in System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

###  <a name="BKMK_RunningReports"></a> Running reports  
 When you run a report in the Configuration Manager console, Report Viewer opens and connects to Reporting Services. After you specify any required report parameters, Reporting Services then retrieves the data and displays the results in the viewer. You can also connect to the SQL Services Reporting Services, connect to the data source for the site, and run reports.  

###  <a name="BKMK_ReportPrompts"></a> Report prompts  
 A report prompt or report parameter in Configuration Manager is a report property that you can configure when a report is created or modified. Report prompts are created to limit or target the data that a report retrieves. A report can contain more than one prompt as long as the prompt names are unique and contain only alphanumeric characters that conform to the SQL Server rules for identifiers.  

 When you run a report, the prompt requests a value for a required parameter and, based on the value, retrieves the report data. For example, the **Computer information for a specific computer** report retrieves the computer information for a specific computer and prompts the administrative user for a computer name. Reporting Services passes the specified value to a variable that is defined in the SQL statement for the report.  

###  <a name="BKMK_ReportLinks"></a> Report links  
 Report links in Configuration Manager are used in a source report to provide administrative users with easy access to additional data, such as more detailed information about each of the items in the source report. If the destination report requires one or more prompts to run, the source report must contain a column with the appropriate values for each prompt. You must specify the column number that provides the value for the prompt. For example, you might link a report that lists computers that were discovered recently to a report that lists the last messages that were received for a specific computer. When the link is created, you might specify that column 2 in the source report contains computer names, which is a required prompt for the destination report. When the source report is run, link icons appear to the left of each row of data. When you click the icon on a row, Report Viewer passes the value in the specified column for that row as the prompt value that is required to display the destination report. A report can be configured with only one link, and that link can connect only to a single destination resource.  

> [!WARNING]  
>  If you move a destination report to a different report folder, the location for the destination report changes. The report link in the source report is not automatically updated with the new location, and the report link will not work in the source report.  

##  <a name="BKMK_ReportFolders"></a> Report folders  
 Report folders in System Center Configuration Manager provide a method to sort and filter reports that are stored in Reporting Services. Report folders are particularly useful when you have many reports to manage. When you install a reporting services point, reports are copied to Reporting Services and organized into more than 50 report folders. The report folders are read-only. You cannot modify them in the Configuration Manager console.  

##  <a name="BKMK_ReportSubscriptions"></a> Report subscriptions  
 A report subscription in Reporting Services is a recurring request to deliver a report at a specific time or in response to an event, and in an application file format that you specify in the subscription. Subscriptions provide an alternative to running a report on demand. On-demand reporting requires that you actively select the report each time you want to view the report. In contrast, subscriptions can be used to schedule and then automate the delivery of a report.  

 You can manage report subscriptions in the Configuration Manager console. They are processed on the report server. The subscriptions are distributed by using delivery extensions that are deployed on the server. By default, you can create subscriptions that send reports to a shared folder or to an email address. For more information about managing report subscriptions, see [Operations and maintenance for reporting in System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_ReportBuilder"></a> Report Builder  
 Configuration Manager uses Microsoft SQL Server Reporting Services Report Builder as the exclusive authoring and editing tool for both model-based and SQL-based reports. When you initiate the action to create or edit a report in the Configuration Manager console, Report Builder opens. When you create or modify a report for the first time, Report Builder is installed automatically. The version of Report Builder associated with the installed version of SQL Server opens when you run or edit reports.  

 The Report Builder installation adds support for over 20 languages. When you run Report Builder, it displays data in the language of the operating system that is running on the local computer. If Report Builder does not support the language, the data is displayed in English. Report Builder supports the full capabilities of SQL Server 2008 Reporting Services, which includes the following capabilities:  

-   Delivers an intuitive report authoring environment with an appearance similar to Microsoft Office.  

-   Offers the flexible report layout of SQL Server 2008 Report Definition Language (RDL).  

-   Provides various forms of data visualization including charts and gauges.  

-   Provides richly formatted text boxes.  

-   Exports to Microsoft Word format.  

 You can also open Report Builder from SQL Server Reporting Services.  

##  <a name="BKMK_ReportModels"></a> Report models in SQL Server Reporting Services  
 SQL Reporting Services in Configuration Manager uses report models to help administrative users select items from the database to include in model-based reports. For the administrative user who is building the report, report models expose only specified views and items to choose from. To create model-based reports, at least one report model has to be available. Report models have the following features:  

-   You can give database fields and views logical business names to facilitate producing reports. Knowledge of the database structure is not required to produce reports.  

-   You can group items logically.  

-   You can define relationships between items.  

-   You can secure model elements so that administrative users can see only the data that they have permission to see.  

 Although Configuration Manager provides sample report models, you can also define report models to meet your own business requirements. For more information about how to create report models, see [Creating custom report models for System Center Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

## Next steps
[Planning for reporting](planning-for-reporting.md)
