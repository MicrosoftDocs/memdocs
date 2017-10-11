---
title: "SQL Server Always On"
titleSuffix: "Configuration Manager"
description: "Plan to use a SQL Server Always On Availability group with SCCM."
ms.custom: na
ms.date: 09/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Prepare to use SQL Server Always On availability groups with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Prepare System Center Configuration Manager to use SQL Server Always On availability groups as a high availability and disaster recovery solution for the site database.  
Configuration Manager supports using availability groups:
-     At primary sites and the central administration site.
-     On-premises, or in Microsoft Azure.

When you use availability groups in Microsoft Azure, you can further increase availability of your site database by using *Azure Availability Sets*. For more information on Azure Availability Sets, see [Manage the availability of virtual machines](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Before you continue, be comfortable with configuring SQL Server and SQL Server availability groups. The information that follows references the SQL Server documentation library and procedures.

## Supported scenarios
The following are supported scenarios for using availability groups with Configuration Manager. Details and procedures for each can be found in [Configure availability groups for Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).


-      [Create an availability group for use with Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Configure a site to use an availability group](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Add or remove synchronous replica members from an availability group that hosts a site database](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members).
-     [Configure asynchronous commit replicas](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (Requires Configuration Manager version 1706 or later.)
-     [Recover a site from an asynchronous commit replica](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (Requires Configuration Manager version 1706 or later.)
-     [Move a site database out of an availability group to a default or named instance of a standalone SQL Server](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## Prerequisites
The following prerequisites apply to all scenarios. If additional prerequisites apply to a specific scenario, those will be detailed with that scenario.   

### Configuration Manager accounts and permissions
**Site server to replica member access:**   
The computer account of the site server must be a member of the **Local Administrators** group on each computer that is a member of the availability group.

### SQL Server
**Version:**  
Each replica in the availability group must run a version of SQL Server that is supported by your version of Configuration Manager. When supported by SQL Server, different nodes of an availability group can run different versions of SQL Server.

**Edition:**  
You must use an *Enterprise* edition of SQL Server.

**Account:**  
Each instance of SQL Server can run under a domain user account (**service account**) or a non-domain account. Each replica in a group can have a different configuration. Per [SQL Server best practices](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd), use an account with the lowest possible permissions.

-   To configure Service Accounts and permissions for SQL Server 2016, see [Configure Windows Service Accounts and Permissions](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) on MSDN.
-  	To use a non-domain account, you must use certificates. For more information, see [Use Certificates for a Database Mirroring Endpoint (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).


For more information see [Create a Database Mirroring Endpoint for Always On Availability Groups](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### Availability group configurations
**Replica members:**  
- 	The availability group must have one primary replica.
- 	Prior to version 1706, you can have up to two synchronous secondary replicas.
- 	Beginning with version 1706, you can use the same number and type of replicas in an availability group as supported by the version of SQL Server that you use.

-   Beginning with version 1706, you can use an asynchronous commit replica to recover your synchronous replica. See [site database recovery options]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) in the Backup and Recovery topic for information on how to accomplish this.
    > [!CAUTION]  
    > Configuration Manager does not support failover to use the asynchronous commit replica as your site database.
Because Configuration Manager does not validate the state of the asynchronous commit replica to confirm it is current, and [by design such a replica can be out of sync]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), use of an asynchronous commit replica as the site database can put the integrity of your site and data at risk.

Each replica member must:
-   Use the **default instance**  
    *Beginning with version 1702, you can use a* ***named instance***.

-	  Have **Connections in Primary Role** set to **Yes**
-	  Have **Readable Secondary** set to **Yes**  
-	  Be set for **Manual Failover** 	  

    >  [!TIP]
    >  Configuration Manager supports using the availability group synchronous replicas when set to **Automatic Failover**. However, **Manual Failover** must be set when:
    >  -  You run Setup to specify use of the site database in the availability group.
    >  -  When you install any update to Configuration Manager (not just updates that apply to the site database).  

**Replica member location:**  
All replicas in an availability group must be hosted on-premises or hosted on Microsoft Azure. A group that includes an on-premises member and a member in Azure is not supported.     

When you set up an availability group in Azure and the group is behind an internal or external load balancer, the following are default ports you must open to enable Setup access to each replica:   

-	  RCP Endpoint Mapper - **TCP 135**   
-	  Server Message Block – **TCP 445**  
    *You can remove this port after the database move completes. Beginning with version 1702, this port is no longer required.*
-	  SQL Server Service Broker -  **TCP 4022**
-	  SQL over TCP – **TCP 1433**   

After Setup completes,  the following ports must remain accessible:
-	  SQL Server Service Broker -  **TCP 4022**
-	  SQL over TCP – **TCP 1433**

Beginning with version 1702, you can use custom ports for these configurations. The same ports must be used by the endpoint, and on all replicas in the availability group.


**Listener:**   
The availability group must have at least one **availability group listener**. The virtual name of this listener is used when you configure Configuration Manager to use the site database in the availability group. Although an availability group can contain multiple listeners, Configuration Manager can only make use of one. See [Create or Configure an Availability Group Listener (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server) for more information.

**File paths:**   
When you run Configuration Manager Setup to configure a site to use the database in an availability group, each secondary replica server must have a SQL Server file path that is identical to the file path for the site database files as found on the current primary replica.
-   If an identical path does not exist, Setup will fail to add the instance for the availability group as the new location of the site database.
-   Additionally, the local SQL Server service account must have **Full Control** permission to this folder.

The secondary replica servers only require this file path while you are using Setup to specify the database instance in the availability group. After Setup completes configuration of the site database in the availability group, you can delete the unused path from secondary replica severs.

For example, consider the following scenario:
-	You create an availability group that uses three SQL Servers.

-	Your primary replica server is a new installation of SQL Server 2014. By default, the database .MDF and .LDF files are stored in C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA.

-	Both of your secondary replica servers were upgraded to SQL Server 2014 from previous versions, and retain the original file path to store database files of: C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA.

-	Before you attempt to move the site database to this availability group, on each secondary replica server you must create the following file path even if the secondary replicas will not use this file location: C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (this is a duplicate of the path that is in use on the primary replica).

-	You then grant the SQL Server service account on each secondary replica full control access to the newly created file location on that server.

-	You can now successfully run Configuration Manager Setup to configure the site to use the site database in the availability group.

**Configure the database on a new replica:**   
 The database of each replica must be set with the following:
- 	**CLR Integration** must be *enabled*
-	  **Max text repl size** must be *2147483647*
-	  The database owner must be the *SA account*
-	  **TRUSTWORTY** must be **ON**
-	  **Service Broker** must be *enabled*

You can make these configurations on only a primary replica. To configure a secondary replica, you must first failover the primary to the secondary to make the secondary which makes the secondary the new primary replica.   

Use SQL Server documentation when necessary to help you configure the settings. For example, see [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) or [CLR Integration](/sql/relational-databases/clr-integration/clr-integration-enabling) in the SQL Server documentation.

### Verification script
You can run the following script to verify database configurations for both primary and secondary replicas. Before you can fix an issue on a secondary replica, you must change that secondary replica to be the primary replica.

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:

## Limitations and known issues
The following limitations apply to all scenarios.   

**SQL Server options and configurations that are not supported:**
- **Basic availability groups**  
  Introduced with SQL Server 2016 Standard edition, [basic availability groups](https://msdn.microsoft.com/library/mt614935.aspx) do not support read access to secondary replicas, a requirement for use with Configuration Manager.
- **Failover Cluster Instance**  
  [Failover Cluster Instances](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server) are not supported for a replica you use with Configuration Manager.

**SQL servers that host additional availability groups:**   
Prior to Configuration Manager version 1610, when an availability group on a SQL Server  hosts one or more availability groups in addition to the group you use for Configuration Manager, each replica in each of those additional availability groups must have the following configurations set at the time you run Configuration Manager Setup or install an update for Configuration Manager:
-   **Manual Failover**
- 	**allow any read-only connection**

**Non-supported database use:**
-   **Configuration Manager supports only the site database in an availability group:** The following are not supported:
    -   Reporting database
    -   WSUS database
-   **Pre-existing database:** You cannot use new database created on the replica. Instead, you must restore a copy of an existing Configuration Manager database to the primary replica when configuring an availability group.

**Setup errors in ConfigMgrSetup.log:**  
When you run Setup to move a site database to an availability group, Setup tries to process database roles on the secondary replicas of the availability group and logs errors like the following:
-   ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)  

These errors are safe to ignore.

## Changes for site backup
**Backup database files:**  
When a site database runs in an availability group, you should run the built-in **Backup Site server** maintenance task to backup common Configuration Manager settings and files. However, do not use the .MDF or .LDF files created by that backup. Instead, make direct backups of these database files by using SQL Server.

**Transaction log:**  
The recovery model of the site database must be set to **Full** (a requirement for use in an availability group). With this configuration, plan to monitor and maintain the size of the site database transaction log. In the full recovery model, the transactions are not hardened until a full backup of the database or transaction log is made. See [Back Up and Restore of SQL Server Databases](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) in the SQL Server documentation for more information.

## Changes for site recovery
You can use the site recovery option **Skip database recovery (Use this option if the site database was unaffected)** if at least one node of the availability group remains functional.

 Before you can recover the site when all nodes of an availability group have been lost, you must recreate the availability group. Configuration Manager cannot rebuild or restore the availability node. After the group is recreated, and a backup restored and reconfigured, you can then use the site recovery option **Skip database recovery (Use this option if the site database was unaffected)**.

For more information, see [Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## Changes for reporting
**Install the reporting service point:**  
The reporting services point does not support using the listener virtual name of the availability group or the hosting of the reporting services database in a SQL Server Always On availability group:
-   By default, the reporting services point installation sets the **Site database server name** to the virtual name that is specified as the listener. Change this to specify a computer name and instance of a replica in the availability group.
-   To offload the reporting load and to increase availability when a replica node is offline, consider installing additional reporting services points on each replica node and configuring each reporting services point to point to its own computer name.

When you install a reporting service point on each replica of the availability group, reporting can always connect to an active reporting point server.

**Switch the reporting services point used by the console:**  
To run reports, in the console go to **Monitoring** > **Overview** > **reporting** > **Reports**, and then choose **Report Options**. In the Report Options dialog box, select the desired reporting services point.

## Next steps
After you understand the prerequisites, limitations, and changes to common tasks that are required when you use availability groups, see [Configure availability groups for Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag), for procedures to set up and configure your site to use availability groups.
