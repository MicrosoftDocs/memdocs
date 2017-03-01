---
title: "Data warehouse| Microsoft Docs"
description: "Data warehouse service point and database for System Center Configuration Manager"
ms.custom: na
ms.date: 3/27/2017
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
#  The Data Warehouse Service point for System Center Configuration Manager
*Applies to: System Center Configuration Manager (Current Branch)*

Begning with version 1702 you can use the Data Warehouse Service point to store and report on long-term historical data for your Configuration Manager deployment.

> [!TIP]  
> Introduced with version 1610, the data warehouse service point is a pre-release feature. To enable it, see [Use pre-release features](/sccm/core/servers/manage/pre-release-features).

The data warehouse supports up to 2 TB of data, with timestamps for change tracking. Storage of data is accomplished by automated synchronizations from the Configuration Manager site database to the data warehouse database. This information is then accessible from your reporting services point.


Data that is synchronized includes the following from the Global Data and Site Data groups:
- Infrastructure health
- Security
- Compliance
- Malware   
- Software deployments
- Inventory details (however, inventory history is not synchronized)

When the site system role installs, it installs and configures the data warehouse database. It also installs several new reports so you can easily search for and report on this data.



## Prerequisites for the Data Warehouse Service point
- The computer where you install the site system role requires .NET Framework 4.5.2 or later.
- The computer account of the computer where you install the site system role is used to synchronize data with the data warehouse database. This account requires the following permissions:  
  - **Administrator** on the computer that will host the data warehouse database.
  - **DB_owner** permission on the data warehouse database.
-	Your hierarchy must have a Reporting Services point site system role installed before you can install the data warehouse.
-	The data warehouse database is supported on a default or named instance of SQL Server 2012 or later. The edition must be Enterprise or Datacenter.
  - SQL Server Cluster:  This configuration should work, but has not been tested.
  - SQL Server AlwaysOn availability group: This configuration is not supported.


## Install the Data Warehouse
You can install the Data Warehouse site system role at the top-tier site of your hierarchy (a central administration site or stand-alone primary site).

Each hierarchy supports a single instance of this role, and it can be located on any site system. The SQL Server that hosts the database for the warehouse can be local to the site system role, or remote. Although you must have a Reporting Services point installed before you can install the data warehouse service point, the data warehouse service point does not need to be installed on the same server as the reporting services point.

To install the role, use the **Add Site System Roles Wizard** or the **Create Site System Server Wizard**. See [Install site system roles](/sccm/core/servers/deploy/configure/install-site-system-roles) for more information.  

When you install the role, Configuration Manager creates the data warehouse database for you on the instance of SQL Server that you specify. If you specify the name of an existing database (as you would do if you [move the data warehouse database to a new SQL Server](#move-the-data-warehouse-database)), Configuration Manager doesn’t create a new database but instead uses the one you specify.

### Configurations used during installation
**System Role Selection** page:  
Before the Wizard displays the *Data Warehouse Service point*, the site must have a reporting services point.

**General** page:
- 	**Configuration Manager data warehouse database connection settings**:
 - **SQL Server fully qualified domain name**:  
 Specify the full qualified domain name (FQDN) of the server that hosts the data warehouse service database.
 - **SQL Server instance name, if applicable**:   
 If you do not use a default instance of SQL Server, you must specify the instance.
 - **Database name**:   
 Specify a name for the data warehouse database.  Configuration Manager will create the data warehouse database with this name. If you specify a database name that already exists on the instance of SQL server, Configuration Manager will use that database.
 - **SQL Server port used for connection**:   

Specify the TCP/IP port number that is configured for the SQL Server that hosts the data warehouse datbase. This port is used by the data warehouse synchronization service to connect to the data warehouse database.  

**Synchronization schedule** page:   
- **Synchronization schedule**:
 - **Start time**:  
 Specify the time that you want the data warehouse synchronization to start.
 - **Recurrence Pattern**:
    - **Daily**: Specify that synchronization runs every day.
    - **Weekly**: Specify a single day each week, and weekly recurrence for synchronization.

  ## Reporting
After you install a Data Warehouse site system role, the following reports are available on your reporting services point with a Category of **Data Warehouse**:
 - **Application Deployment Report**:   
 View details for application deployment for a specific application and machine.
 - **Endpoint Protection and Software Update Compliance Report**:
  View computers that are missing software updates.  
 - **General Hardware Inventory Report**:	  
 View all hardware inventory for a specific machine.
 - **General Software Inventory Report**:	  
 View all software inventory for a specific machine.
 - **Infrastructure Health Overview**:	 
 Displays an overview of the health of your Configuration Manager infrastructure
 - **List of Malware Detected**:	 
 View malware that has been detected in the organization.
 - **Software Distribution Summary Report**:	 
 A summary of software distribution for a specific advertisement and machine.

## Move the Data Warehouse database
Use the following steps to move the data warehouse database to a new SQL Server:

1.	Use SQL Server Management Studio to backup the data warehouse database, and then restore that database to a SQL Server on the new computer that will host the data warehouse.   

> [!NOTE]     
> After you restore the database to the new server, ensure that the database access permissions are the same on the new data warehouse database as they were on the original data warehouse database.

2.	Use the Configuration Manager console to remove the Data Warehouse Service point site system role from the current server.
3.	Reinstall the Data Warehouse Service point and specify the name of the new SQL Server and instance that hosts the Data Warehouse database you restored.
4.	After the site system role installs, the move is complete.

## Troubleshooting data warehouse issues
**Log Files**:  
Use the following logs to investigate problems with the installation of the Data Warehouse Service point, or synchronization of data:
 - *DWSSMSI.log* and *DWSSSetup.log* - Use these logs to investigate errors when installing the Data warehouse service point.
 - *Microsoft.ConfigMgrDataWarehouse.log* – Use this log to investigate data synchronization between the site database to the data warehouse database.

**Known synchronization issues**:   
Synchronization fails with the following in the *Microsoft.ConfigMgrDataWarehouse.log*: **“failed to populate schema objects”**  
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
  2.	On the computer that hosts SQL Server Reporting Services, open the MMC and add the snap-in for **Certificates**, and then select to manage certificate for **Computer account**. Under the **Trusted Root Certificate Authorities** folder, import the **Data Warehouse SQL Server Identification Certificate**.

 
## Data Warehouse Dataflow   
![Datawarehouse_flow](./media/datawarehouse.png)

**Data storage and synchronization**

| Step   | Details  |
|:------:|-----------|  
| **1**  | 	The site server transfers and stores data in the site database.  |  
| **2**  |  	Based on its schedule and configuration, the Data Warehouse Service point gets data from the site database.  |  
| **3**  |  The Data Warehouse Service point transfers and stores a copy of the synchronized data in the Data Warehouse database. |  
**Reporting**

| Step   | Details  |
|:------:|-----------|  
| **A**  |  Using built-in reports, a user requests data. This request is passed to the Reporting Services point using SQL Server Reporting Services. |  
| **B**  |  	Most reports are for current information, and these requests are run against the site database. |  
| **C**  | When a report requests historical data, by using one of the reports with a *Category* of **Data Warehouse**, the request is run against the Data Warehouse database.   |  
