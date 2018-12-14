---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: Plan to use a SQL Server Always On availability group with Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Prepare to use SQL Server Always On availability groups with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use this article to prepare Configuration Manager to use SQL Server Always On availability groups. This feature provides a high availability and disaster recovery solution for the site database.  

Configuration Manager supports using availability groups:
- At primary sites and the central administration site.
- On-premises, or in Microsoft Azure.

When you use availability groups in Microsoft Azure, you can further increase availability of your site database by using *Azure Availability Sets*. For more information on Azure Availability Sets, see [Manage the availability of virtual machines](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
>  Before you continue, be comfortable with configuring SQL Server and SQL Server availability groups. The information that follows references the SQL Server documentation library and procedures.



## Supported scenarios

The following scenarios are supported for using availability groups with Configuration Manager. For more information and procedures for each scenario, see [Configure availability groups for Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).

- [Create an availability group for use with Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group)  
- [Configure a site to use an availability group](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group)  
- [Add or remove synchronous replica members from an availability group that hosts a site database](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members)  
- [Configure asynchronous commit replicas](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca)  
- [Recover a site from an asynchronous commit replica](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site)  
- [Move a site database out of an availability group to a default or named instance of a standalone SQL Server](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group)  



## Prerequisites

The following prerequisites apply to all scenarios. If additional prerequisites apply to a specific scenario, they're detailed with that scenario.   

### Configuration Manager accounts and permissions

#### Site server to replica member access   
The computer account of the site server must be a member of the **Local Administrators** group on each computer that's a member of the availability group.


### SQL Server

#### Version  
Each replica in the availability group must run a version of SQL Server that's supported by your version of Configuration Manager. When supported by SQL Server, different nodes of an availability group can run different versions of SQL Server. For more information, see [Supported SQL Server versions for Configuration Manager](/sccm/core/plan-design/configs/support-for-sql-server-versions).<!--SCCMDocs issue 656-->

#### Edition  
Use an *Enterprise* edition of SQL Server.

#### Account  
Each instance of SQL Server can run under a domain user account (**service account**) or a non-domain account. Each replica in a group can have a different configuration. 

- Use an account with the lowest possible permissions. For more information, see [Security considerations for a SQL Server installation](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- For more information on configuring service accounts and permissions for SQL Server, see [Configure Windows service accounts and permissions](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- To use a non-domain account, you must use certificates. For more information, see [Use certificates for a database mirroring endpoint (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- For more information, see [Create a Database Mirroring Endpoint for Always On Availability Groups](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### Availability group configurations

#### Replica members  
- The availability group must have one primary replica.  

- Use the same number and type of replicas in an availability group that your version of SQL Server supports.

- You can use an asynchronous commit replica to recover your synchronous replica. For more information, see [site database recovery options](/sccm/core/servers/manage/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).  

    > [!Warning]  
    > Configuration Manager doesn't support *failover* to use the asynchronous commit replica as your site database. For more information, see [Failover and failover modes (Always On availability groups)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups?view=sql-server-2014).  

Configuration Manager doesn't validate the state of the asynchronous commit replica to confirm it's current. Use of an asynchronous commit replica as the site database can put the integrity of your site and data at risk. By design, such a replica can be out of sync. For more information, see [Overview of SQL Server AlwaysOn availability groups](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Each replica member must have the following configuration:

- Use the *default instance* or a *named instance*  

- The **Connections in Primary Role** setting is **Yes**  

- THe **Readable Secondary** setting is **Yes**  

- Enabled for **Manual Failover** 	  

  > [!TIP]
  >  Configuration Manager supports using the availability group synchronous replicas when set to **Automatic Failover**. Set **Manual Failover** when:
  >  -  You run Configuration Manager Setup to specify use of the site database in the availability group.  
  >  -  You install any update to Configuration Manager. (Not just updates that apply to the site database).  

#### Replica member location
Either host all replicas in an availability group on-premises, or host them all on Microsoft Azure. A group that includes an on-premises member and a member in Azure isn't supported.     

Configuration Manager Setup needs to connect to each replica. When you set up an availability group in Azure, and the group is behind an internal or external load balancer, open the following default ports:   

- RCP Endpoint Mapper: **TCP 135**   

- SQL Server Service Broker: **TCP 4022**  

- SQL over TCP: **TCP 1433**   


After Setup completes, the following ports must stay open for Configuration Manager:  

- SQL Server Service Broker: **TCP 4022**  

- SQL over TCP: **TCP 1433**  

You can use custom ports for these configurations. Use the same custom ports by the endpoint and on all replicas in the availability group.


#### Listener   
The availability group must have at least one *availability group listener*. When you configure Configuration Manager to use the site database in the availability group, it uses the virtual name of this listener. Although an availability group can contain multiple listeners, Configuration Manager can only make use of one. For more information, see [Create or configure a SQL Server availability group listener](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### File paths   
When you run Configuration Manager Setup to configure a site to use the database in an availability group, each secondary replica server must have a SQL Server file path that's identical to the file path for the site database files on the current primary replica. If an identical path doesn't exist, Setup fails to add the instance for the availability group as the new location of the site database.  

The local SQL Server service account must have **Full Control** permission to this folder.

The secondary replica servers only require this file path while you're using Configuration Manager Setup to specify the database instance in the availability group. After it completes configuration of the site database in the availability group, you can delete the unused path from secondary replica severs.

For example, consider the following scenario:

- You create an availability group that uses three SQL Servers.  

- Your primary replica server is a new installation of SQL Server 2014. By default, it stores the database .MDF and .LDF files in `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- You upgraded both of your secondary replica servers to SQL Server 2014 from previous versions. With the upgrade, these servers keep the original file path to store database files: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Before move the site database to this availability group, on each secondary replica server, create the following file path: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. This path is a duplicate of the path in use on the primary replica, even if the secondary replicas won't use this file location.  

- You then grant the SQL Server service account on each secondary replica full control access to the newly created file location on that server.  

- You can now successfully run Configuration Manager Setup to configure the site to use the site database in the availability group.  

#### Configure the database on a new replica   
 Configure the database of each replica with the following settings:  

- Enable **CLR Integration**. For more information, see [CLR integration](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Set **Max text repl size** to `2147483647`  

- Set the database owner to the *SA account*  

- Turn **ON** the **TRUSTWORTY** setting. For more information, see the [TRUSTWORTHY database property](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).   

- Enable the **Service Broker**  

Only make these configurations on a primary replica. To configure a secondary replica, first fail over the primary to the secondary. This action makes the secondary the new primary replica.   


### Verification script

Run the following SQL script to verify database configurations for both primary and secondary replicas. Before you can fix an issue on a secondary replica, change that secondary replica to be the primary replica.

```SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

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
```



## Limitations and known issues

The following limitations apply to all scenarios.   

#### Unsupported SQL Server options and configurations

- **Basic availability groups**: Introduced with SQL Server 2016 Standard edition, basic availability groups don't support read access to secondary replicas. Configuration requires this access. For more information, see [Basic SQL Server availability groups](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Failover cluster instance**: Failover cluster instances aren't supported for a replica you use with Configuration Manager. For more information, see [SQL Server Always On failover cluster instances](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: It's not supported to use an availability group with Configuration Manager in a multi-subnet configuration. You also can't use the [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) keyword connection string.  

#### SQL Servers that host additional availability groups
<!--SCCMDocs issue 649-->
When the SQL Server hosts one or more availability groups in addition to the group you use for Configuration Manager, it needs specific settings at the time you run Configuration Manager Setup. These settings are also needed to install an update for Configuration Manager. Each replica in each availability group must have the following configurations:

- Manual Failover  
- Allow any read-only connection  

#### Unsupported database use

- **Configuration Manager supports only the site database in an availability group:** The following databases aren't supported by Configuration Manager in a SQL Server Always On availability group:  
    - Reporting database  
    - WSUS database  

- **Pre-existing database:** You can't use a new database created on the replica. When you configure an availability group, restore a copy of an existing Configuration Manager database to the primary replica.  

#### Setup errors in ConfigMgrSetup.log  
When you run Configuration Manager Setup to move a site database to an availability group, it tries to process database roles on the secondary replicas of the availability group. The **ConfigMgrSetup.log** file shows the following error:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

These errors are safe to ignore.

#### Site expansion
<!--SCCMDocs issue 568-->
If you configure the site database for a standalone primary site to use SQL Always On, you can't expand the site to include a central administration site. If you try this process, it fails. To expand the site, temporarily remove the primary site database from the availability group.



## Changes for site backup

### Backup database files
  
When a site database uses an availability group, run the built-in **Backup Site server** maintenance task to back up common Configuration Manager settings and files. Don't use the .MDF or .LDF files created by that backup. Instead, make direct backups of these database files by using SQL Server.


### Transaction log  

Set the recovery model of the site database to **Full**. This configuration is a requirement for Configuration Manager use in an availability group. Plan to monitor and maintain the size of the site database transaction log. In the full recovery model, the transactions aren't hardened until it makes a full backup of the database or transaction log. For more information, see [Back up and restore of SQL Server databases](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).



## Changes for site recovery

If at least one node of the availability group is still functional, use the site recovery option to **Skip database recovery (Use this option if the site database was unaffected)**.

When you lose all nodes of an availability group, before you can recover the site, first recreate the availability group. Configuration Manager can't rebuild or restore the availability node. Recreate the group, restore the backup, and reconfigure SQL. Then use the site recovery option to **Skip database recovery (Use this option if the site database was unaffected)**.

For more information, see [Backup and recovery](/sccm/core/servers/manage/backup-and-recovery).



## Changes for reporting

### Install the reporting service point

The reporting services point doesn't support using the listener virtual name of the availability group. It also doesn't support hosting its database in a SQL Server Always On availability group.  

- By default, the reporting services point installation sets the **Site database server name** to the virtual name that's specified as the listener. Change this setting to specify a computer name and instance of a replica in the availability group.  

- To offload reporting and to increase availability when a replica node is offline, consider installing additional reporting services points on each replica node. Then configure each reporting services point to use its own computer name. When you install a reporting service point on each replica of the availability group, reporting can always connect to an active reporting point server.  


### Switch the reporting services point used by the console

1. In the Configuration Manager console, go to the **Monitoring** workspace.  

2. Expand **Reporting** and select **Reports**.  

3. Click **Report Options**.  

4. In the Report Options dialog box, select the reporting services point you want to use.  



## Next steps

This article described the prerequisites, limitations, and changes to common tasks that Configuration Manager requires when you use availability groups. For procedures to set up and configure your site to use availability groups, see [Configure availability groups](/sccm/core/servers/deploy/configure/configure-aoag).
