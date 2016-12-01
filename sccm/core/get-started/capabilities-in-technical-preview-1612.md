---
title: "Capabilities in Technical Preview 1612 for System Center Configuration Manager | Microsoft Docs"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1612."
ms.custom: na
ms.date: 12/16/2016
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
caps.latest.revision: 5
author: Brendunsms.author: brendunsmanager: angrobe
---
# Capabilities in Technical Preview 1612 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*



This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1612. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## The Data Warehouse Service point

Beginning with the Technical Preview version 1612, the Data Warehouse Service point enables you to store and report on long-term historical data for your Configuration Manager deployment. This is accomplished by automated synchronizations from the Configuration Manager site database to a data warehouse database. This information is then accessible from your Reporting services point.

By default, when you install the new site system role, Configuration Manager creates the data warehouse database for you on a SQL Server instance that you specify. The data warehouse supports up to 2 TB of data, with timestamps for change tracking.  By default, the data that is synchronized from the site database includes the data groups for Global Data, Site Data, Global_Proxy, Cloud Data, and Database Views. You can also modify what is synchronized to include additional tables, or exclude specific tables from the default replication sets.
The default data that is synchronized includes information about:
- Infrastructure health
- Security
- Compliance
- Malware   
- Software deployments
- Inventory details (however, inventory history is not synchronized)

In addition to installing and configuring the data warehouse database, several new reports are installed so you can easily search for and report on this data.

### Data Warehouse Dataflow   
![Datawarehouse_flow](./media/datawarehouse.png)


| Step         | Details  |
|:------:|-----------|  
| **1**  | 	The site server transfers and stores data in the site database.  |  
| **2** |  	Based on its schedule and configuration, the Data Warehouse Service point gets data from the site database.  |  
| **3** |  The Data Warehouse Service point transfers and stores a copy of the synchronized data in the Data Warehouse database. |  
| **A** |  Using built-in reports, a request for data is made which is passed to the Reporting Services point using SQL Server Reporting Services. |  
| **B** |  	Most reports are for current information, and these requests are run against the site database. |  
| **C** | When a report requests historical data, by using one of the reports with a *Category* of **Data Warehouse**, the request is run against the Data Warehouse database.   |  


### Prerequisites for the Data Warehouse Service point and database
- Your hierarchy must have a Reporting services point site system role installed.
- The computer where you install the site system role requires .NET Framework 4.5.2 or later.
- The computer account of the computer where you install the site system role must have local admin permissions to the computer that will host the data warehouse database.
- The administrative account you use to install the site system role must be a DBO on the instance of SQL Server that will host the data warehouse database.  
-  The database is supported:
  - With SQL Server 2012 or later, Enterprise or Datacenter edition.
  - On a default or named instance
  - On a *SQL Server Cluster*. Although this configuration should work, it has not been tested and support is best effort.
  - When co-located with either the site database or Reporting services point database. However, we recommend it be installed on a separate server.  
- The database is not supported on a *SQL Server AlwaysOn availability group*.

### Install the Data Warehouse
You install the Data Warehouse site system role on a central administration site or primary site by using the **Add Site System Roles Wizard** or the **Create Site System Server Wizard**. See [Install site system roles](/sccm/core/servers/deploy/configure/install-site-system-roles) for more information. A hierarchy supports multiple instances of this role, but only one instance is supported at each site.  

When you install the role, Configuration Manager creates the data warehouse database for you on the instance of SQL Server that you specify. If you specify the name of an existing database (as you would do if you [move the data warehouse database to a new SQL Server](#move-the-data-warehouse-database)), Configuration Manager doesn’t create a new database but instead uses the one you specify.

#### Configurations used during installation
Use the following information to complete installation of the site system role:

**System Role Selection** page:  
Before the Wizard displays an option to select and install the Data Warehouse Service point, you must have installed a Reporting services point.

**General** page: The following general information is required:
- **Configuration Manager database settings:**   
  - **Server Name** - Specify the FQDN of the server that hosts the site database. If you do not use a default instance of SQL Server, you must specify the instance after the FQDN in the following format: ***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **Database name** - Specify the name of the site database.
  -	**Verify** - Click **Verify** to make sure that the connection to the site database is successful.
</br></br>
- **Data Warehouse database settings:**
  -	**Server name** - Specify the FQDN of the server that hosts the Data Warehouse Service point and database. If you do not use a default instance of SQL Server, you must specify the instance after the FQDN in the following format: ***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  -	**Database name** - Specify the FQDN for the data warehouse database.  Configuration Manager will create the database with this name. If you specify a database name that already exists on the instance of SQL server, Configuration Manager will use that database.
  -	**Verify** - Click **Verify** to make sure that the connection to the site database is successful.

**Synchronization settings** page:   
- **Data settings:**
  - **Replication groups to synchronize** – Select the data groups you want to synchronize. For information about the different types of data groups, see [Database replication](/sccm/core/servers/manage/data-transfers-between-sites#a-namebkmkdbrepa-database-replication) and **Distributed views** in [Data transfers between sites](/sccm/core/servers/manage/data-transfers-between-sites).
  - **Tables included to synchronize** – Specify the name of each additional table you want to synchronize. Separate multiple tables by using a comma. These tables will be synchronized from the site database in addition to the replication groups you select.
  - **Tables excluded to synchronize** - Specify the name of individual tables from replication groups you synchronize. Tables you specify will be excluded from. Separate multiple tables by using a comma.
- **Synchronization settings:**
  - **Synchronization interval (minutes)** - Specify a value in minutes. After the interval is reached, a new synchronization starts. This supports a range from 60 to 1440 minutes (24 hours).
  - **Schedule** - Specify the days that you want synchronization to run.


#### Troubleshoot installation and data synchronization
Use the following logs to investigate problems with the installation of the Data Warehouse Service point, or synchronization of data:
- **DWSSMSI.log** and **DWSSSetup.log**  - Use these logs to investigate errors when installing the Data warehouse service point.
- 	**Microsoft.ConfigMgrDataWarehouse.log** – Use this log to investigate data synchronization between the site database to the data warehouse database.

### Reporting
After you install a Data Warehouse site system role, the following reports are available on your Reporting services point with a *Category* of **Data Warehouse:**

|Report                   | Details                                  |
|-------------------------|------------------------------------------|
| **Application Deployment Report** | View details for application deployment for a specific application and machine.|
| **Endpoint Protection and Software Update Compliance Report**   | View computers that are missing software updates.|
| **General Hardware Inventory Report**  | View all hardware inventory for a specific machine.|
| **General Software Inventory Report**  | View all software inventory for a specific machine.|
| **Infrastructure Health Overview**  |Displays an overview of the health of your Configuration Manager infrastructure.|
| **List of Malware Detected**  |View malware that has been detected in the organization.|
|** Software Distribution Summary Report** | A summary of software distribution for a specific advertisement and machine.|

### Move the Data Warehouse database
Use the following steps to move the data warehouse database to a new SQL Server:

  1. Review the current database configuration and record the configuration details, including:  
   - The data groups you synchronize
   - Tables you include or exclude from synchronization       

   You will reconfigure these data groups and tables after you restore the database to a new server and reinstall the site system role.  

  2. Use SQL Server Management Studio to backup the data warehouse database, and then again to restore that database to a SQL server on the new computer that will host the data warehouse.

  After you restore the database to the new server, ensure that the database access permissions are the same on the new data warehouse database as they were on the original data warehouse database.

  3. Use the Configuration Manager console to remove the Data Warehouse Service point site system role from the current server.

  4. Install a new Data Warehouse Service point and specify the name of the new SQL Server and instance that hosts the Data Warehouse database you restored.

  5. After the site system role installs, the move is complete.

You can review the following Configuration Manager logs to confirm the site system role has successfully reinstalled:  
- **DWSSMSI.log** and **DWSSSetup.log**  - Use these logs to investigate errors when installing the Data warehouse service point.
- 	**Microsoft.ConfigMgrDataWarehouse.log** – Use this log to investigate data synchronization between the site database to the data warehouse database.
