---
title: "Data warehouse"
titleSuffix: "Configuration Manager"
description: "Data Warehouse service point and database for System Center Configuration Manager"
ms.custom: na
ms.date: 8/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision:
author: Brenduns
ms.author: brenduns
manager: angrobe

---
#  The Data Warehouse service point for System Center Configuration Manager
*Applies to: System Center Configuration Manager (Current Branch)*

Beginning with version 1702 you can use the Data Warehouse service point to store and report on long-term historical data for your Configuration Manager deployment.

> [!TIP]
> The Data Warehouse service point is a pre-release feature introduced in version 1702. To enable it, see [Use pre-release features](/sccm/core/servers/manage/pre-release-features).

> Beginning with version 1706, this feature is no longer a pre-release feature.

The data warehouse supports up to 2 TB of data, with timestamps for change tracking. Storage of data is accomplished by automated synchronizations from the Configuration Manager site database to the data warehouse database. This information is then accessible from your Reporting Services point. Data that is synchronized to the data warehouse database is retained for three years. Periodically, a built-in task removes data that is older than three years.

Data that is synchronized includes the following from the Global Data and Site Data groups:
- Infrastructure health
- Security
- Compliance
- Malware   
- Software deployments
- Inventory details (however, inventory history is not synchronized)

When the site system role installs, it installs and configures the data warehouse database. It also installs several reports so you can easily search for and report on this data.



## Prerequisites for the Data Warehouse service point
- The data warehouse site system role is supported only at the top-tier site of your hierarchy. (A central administration site or stand-alone primary site).
- The computer where you install the site system role requires .NET Framework 4.5.2 or later.
- The computer account of the computer where you install the site system role is used to synchronize data with the data warehouse database. This account requires the following permissions:  
  - **Administrator** on the computer that will host the data warehouse database.
  - **DB_Creator** permission on the data warehouse database.
  - Either **DB_owner** or **DB_reader** with **execute** permissions to the top-tier sites site database.
- The data warehouse database requires the use of SQL Server 2012 or later. The edition can be Standard, Enterprise, or Datacenter.
- The following SQL Server configurations are supported to host the warehouse database:  
  - A default instance
  - Named instance
  - SQL Server Always On availability group
  - SQL Server failover cluster
-	When the data warehouse database is remote from the site server database, you must have a separate license for each SQL Server that hosts the database.
- If you use [distributed views](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), the data warehouse service point site system role must install on the same server that hosts the central administration sites site database.



> [!IMPORTANT]  
> The Data Warehouse is not supported when the computer that runs the Data Warehouse service point or that hosts the data warehouse database runs one of the following languages:
> - JPN – Japanese
> - KOR – Korean
> - CHS – Simple Chinese
> - CHT – Traditional Chinese
> This issue will be resolved in a future release.


## Install the Data Warehouse
Each hierarchy supports a single instance of this role, on any site system of the top-tier site. The SQL Server that hosts the database for the warehouse can be local to the site system role, or remote. Although the data warehouse works with the Reporting Services point that is installed at the same site, the two site system roles do not need to be installed on the same server.   

To install the role, use the **Add Site System Roles Wizard** or the **Create Site System Server Wizard**. See [Install site system roles](/sccm/core/servers/deploy/configure/install-site-system-roles) for more information.  

When you install the role, Configuration Manager creates the data warehouse database for you on the instance of SQL Server that you specify. If you specify the name of an existing database (as you would do if you [move the data warehouse database to a new SQL Server](#move-the-data-warehouse-database)), Configuration Manager doesn’t create a new database but instead uses the one you specify.

### Configurations used during installation
**System Role Selection** page:  

**General** page:
- 	**Configuration Manager data warehouse database connection settings**:
 - **SQL Server fully qualified domain name**:  
 Specify the full qualified domain name (FQDN) of the server that hosts the Data Warehouse service point database.
 - **SQL Server instance name, if applicable**:   
 If you do not use a default instance of SQL Server, you must specify the instance.
 - **Database name**:   
 Specify a name for the data warehouse database. The database name cannot exceed 10 characters. (The supported name length will be increased in a future release).
 Configuration Manager creates the data warehouse database with this name. If you specify a database name that already exists on the instance of SQL server, Configuration Manager uses that database.
 - **SQL Server port used for connection**:   
 Specify the TCP/IP port number that is configured for the SQL Server that hosts the data warehouse database. This port is used by the data warehouse synchronization service to connect to the data warehouse database.  

**Synchronization schedule** page:   
- **Synchronization schedule**:
 - **Start time**:  
 Specify the time that you want the data warehouse synchronization to start.
 - **Recurrence Pattern**:
    - **Daily**: Specify that synchronization runs every day.
    - **Weekly**: Specify a single day each week, and weekly recurrence for synchronization.

## Reporting
After you install a Data Warehouse service point, several reports become available on the Reporting Services point that is installed at the same site. If you install the Data Warehouse service point before installing a Reporting Services point, the reports will be added automatically when you later install the Reporting Services point.

The Data Warehouse site system role includes the following reports, which have a Category of **Data Warehouse**:
 - **Application Deployment - Historical**:   
 View details for application deployment for a specific application and machine.
 - **Endpoint Protection and Software Update Compliance - Historical**:
  View computers that are missing software updates.  
 - **General Hardware Inventory - Historical**:	  
 View all hardware inventory for a specific machine.
 - **General Software Inventory - Historical**:	  
 View all software inventory for a specific machine.
 - **Infrastructure Health Overview - Historical**:	 
 Displays an overview of the health of your Configuration Manager infrastructure
 - **List of Malware Detected - Historical**:	 
 View malware that has been detected in the organization.
 - **Software Distribution Summary - Historical**:	 
 A summary of software distribution for a specific advertisement and machine.


## Expand an existing stand-alone primary into a hierarchy
Before you can install a central administration site to expand an existing stand-alone primary site, you must first uninstall the Data Warehouse service point role. After you install the central administration site, you can then install the site system role at the central administration site.  

Unlike a move of the data warehouse database, this change results in a loss of the historic data you have previously synchronized at the primary site. It is not supported to backup the database from the primary site and restore it at the central administration site.




## Move the Data Warehouse database
Use the following steps to move the data warehouse database to a new SQL Server:

1.	Use SQL Server Management Studio to backup the data warehouse database. Then, restore that database to a SQL Server on the new computer that hosts the data warehouse.   
> [!NOTE]     
> After you restore the database to the new server, ensure that the database access permissions are the same on the new data warehouse database as they were on the original data warehouse database.  

2.	Use the Configuration Manager console to remove the Data Warehouse service point site system role from the current server.
3.	Reinstall the Data Warehouse service point and specify the name of the new SQL Server and instance that hosts the Data Warehouse database you restored.
4.	After the site system role installs, the move is complete.

## Troubleshooting data warehouse issues
**Log Files**:  
Use the following logs to investigate problems with the installation of the Data Warehouse service point, or synchronization of data:
 - *DWSSMSI.log* and *DWSSSetup.log* - Use these logs to investigate errors when installing the Data Warehouse service point.
 - *Microsoft.ConfigMgrDataWarehouse.log* – Use this log to investigate data synchronization between the site database to the data warehouse database.

**Set up Failure**  
 Installation of the Data Warehouse service point fails on a remote site system server when the data warehouse is the first site system role that installs on that computer.  
  - **Solution**:   
    Make sure that the computer you are installing the Data Warehouse service point on already hosts at least one other site system role.  


**Known synchronization issues**:   
Synchronization fails with the following message in *Microsoft.ConfigMgrDataWarehouse.log*: **“failed to populate schema objects”**  
 - **Solution**:  
    Make sure that the computer account of the computer that hosts the site system role is a **db_owner** on the data warehouse database.

Data warehouse reports fail to open when the data warehouse database and reporting service point are on different site systems.  

 - **Solution**:  
    Grant the **Reporting Services Point Account** the **db_datareader** permission on the data warehouse database.

When you open a data warehouse report, the following error is returned:

*An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)*

- **Solution**: Use the following steps to configure certificates:

  1. On the computer that hosts the data warehouse database:

    1. Open IIS, click **Server Certificates**, right-click on **Create Self-Signed Certificate**, and then specify the "friendly name" of the certificate name as **Data Warehouse SQL Server Identification Certificate**. Select the certificate store as **Personal**.
    2. Open **SQL Server Configuration Manager**, under **SQL Server Network Configuration**, right-click to select **Properties** under **Protocols for MSSQLSERVER**. Then, on the **Certificate** tab, select **Data Warehouse SQL Server Identification Certificate** as the certificate, and then save the changes.  
    3. Open **SQL Server Configuration Manager**, under **SQL Server Services**, restart **SQL Server service** and **Reporting Service**.
    4.	Open the Microsoft Management Console (MMC) and add the snap-in for **Certificates**, select to manage the certificate for **Computer account** of the local machine. Then, in the MMC, expand the **Personal** folder > **Certificates**, and export the **Data Warehouse SQL Server Identification Certificate** as a **DER encoded binary X.509 (.CER)** file.    
  2.	On the computer that hosts SQL Server Reporting Services, open the MMC and add the snap-in for **Certificates**. Then, select to manage certificates for **Computer account**. Under the **Trusted Root Certificate Authorities** folder, import the **Data Warehouse SQL Server Identification Certificate**.


## Data Warehouse Dataflow   
![Datawarehouse_flow](./media/datawarehouse.png)

**Data storage and synchronization**

| Step   | Details  |
|:------:|-----------|  
| **1**  | 	The site server transfers and stores data in the site database.  |  
| **2**  |  	Based on its schedule and configuration, the Data Warehouse service point gets data from the site database.  |  
| **3**  |  The Data Warehouse service point transfers and stores a copy of the synchronized data in the Data Warehouse database. |  
**Reporting**

| Step   | Details  |
|:------:|-----------|  
| **A**  |  Using built-in reports, a user requests data. This request is passed to the Reporting Services point using SQL Server Reporting Services. |  
| **B**  |  	Most reports are for current information, and these requests are run against the site database. |  
| **C**  | When a report requests historical data, by using one of the reports with a *Category* of **Data Warehouse**, the request runs against the Data Warehouse database.   |  
