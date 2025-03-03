---
title: Prepare to use an availability group
titleSuffix: Configuration Manager
description: Plan to use a SQL Server Always On availability group for the Configuration Manager site database.
ms.date: 03/25/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Prepare to use a SQL Server Always On availability group with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use this article to prepare Configuration Manager to use a SQL Server Always On availability group for the site database. This feature provides a high availability and disaster recovery solution.

Configuration Manager supports using availability groups:

- At primary sites and the central administration site.
- On-premises, or in Microsoft Azure.

When you use availability groups in Microsoft Azure, you can further increase availability of your site database by using *Azure availability sets*. For more information on Azure availability sets, see [Manage the availability of virtual machines](/azure/virtual-machines/windows/manage-availability).

> [!IMPORTANT]
> Before you continue, be comfortable with configuring SQL Server and availability groups. This article references the SQL Server documentation library with more information and procedures.

## Supported scenarios

The following scenarios are supported for using availability groups with Configuration Manager. For more information and procedures for each scenario, see [Configure availability groups for Configuration Manager](configure-aoag.md).

- [Create an availability group for use with Configuration Manager](configure-aoag.md#bkmk_create)
- [Configure a site to use the availability group](configure-aoag.md#bkmk_configure)
- [Add or remove synchronous replica members from an availability group that hosts a site database](configure-aoag.md#bkmk_sync)
- [Configure or recover a site from an asynchronous commit replicas](configure-aoag.md#bkmk_async)
- [Move a site database out of an availability group to a default or named instance of a standalone SQL Server](configure-aoag.md#bkmk_stop)

## Prerequisites

The following prerequisites apply to all scenarios. If additional prerequisites apply to a specific scenario, they're detailed with that scenario.

### Configuration Manager accounts and permissions

#### Installation account

The account you use to run Configuration Manager setup must be:

- A member of the local **Administrators** group on each computer that's a member of the availability group.
- A **sysadmin** on each instance of SQL Server that hosts the site database.

#### Site server to replica member access

The computer account of the site server must be a member of the local **Administrators** group on each computer that's a member of the availability group.

### SQL Server

#### Version

Each replica in the availability group must run a version of SQL Server that's supported by your version of Configuration Manager. When supported by SQL Server, different nodes of an availability group can run different versions of SQL Server. For more information, see [Supported SQL Server versions for Configuration Manager](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### Edition

Use an *Enterprise* edition of SQL Server.

#### Account

Each instance of SQL Server can run under a domain user account (**service account**) or a non-domain account. Each replica in a group can have a different configuration.

- Use an account with the lowest possible permissions. For more information, see [Security considerations for a SQL Server installation](/sql/sql-server/install/security-considerations-for-a-sql-server-installation).

- For more information on configuring service accounts and permissions for SQL Server, see [Configure Windows service accounts and permissions](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).

- To use a non-domain account, you must use certificates. For more information, see [Use certificates for a database mirroring endpoint (Transact-SQL)](/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).

- For more general information, see [Create a database mirroring endpoint for availability groups](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### Database

#### Configure the database on a new replica

Only make these configurations on a primary replica. To configure a secondary replica, first fail over the primary to the secondary. This action makes the secondary the new primary replica.

Configure the database of each replica with the following settings:

- Enable **CLR Integration**:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    For more information, see [CLR integration](/sql/relational-databases/clr-integration/clr-integration-enabling).

- Set **Max text repl size** to `2147483647`:

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Set the database owner to the *SA account*. You don't need to enable this account.

- Turn **ON** the **TRUSTWORTHY** setting:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    For more information, see the [TRUSTWORTHY database property](/sql/relational-databases/security/trustworthy-database-property).

- Enable the **Service Broker**:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!NOTE]
    > You can't enable the Service Broker option on a database that's already part of an availability group. You have to enable that option before adding it to the availability group.<!-- SCCMDocs#1432 -->

- Configure the Service Broker priority:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE
    ```

#### Database verification script

Run the following SQL script to verify database configurations for both primary and secondary replicas. Before you can fix an issue on a secondary replica, change that secondary replica to be the primary replica.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
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

### Availability group configurations

#### Replica members

- The availability group must have one primary replica.

- Use the same number and type of replicas in an availability group that your version of SQL Server supports.

- You can use an asynchronous commit replica to recover your synchronous replica. For more information, see [site database recovery options](../../manage/recover-sites.md#site-database-recovery-options).

    > [!WARNING]
    > Configuration Manager doesn't support *failover* to use the asynchronous commit replica as your site database. For more information, see [Failover and failover modes (Always On availability groups)](/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager doesn't validate the state of the asynchronous commit replica to confirm it's current. Use of an asynchronous commit replica as the site database can put the integrity of your site and data at risk. This replica can be out of sync by design. For more information, see [Overview of SQL Server Always On availability groups](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Each replica member must have the following configuration:

- Use the *default instance* or a *named instance*.

  > [!NOTE]
  > Don't have a file share on the server that's the same name as the SQL Server instance name.<!--9401511-->

- The **Connections in Primary Role** setting is **Allow all connections**.

- The **Readable Secondary** setting is **Yes**.

- Enabled for **Manual Failover**

    > [!NOTE]
    > Configuration Manager supports using the availability group synchronous replicas when set to **Automatic Failover**. Set **Manual Failover** when:
    >
    > - You run Configuration Manager setup to specify use of the site database in the availability group.
    > - You install any update to Configuration Manager. (Not just updates that apply to the site database).

- All members need the same [seeding mode](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).<!-- SCCMDocs-pr#3899 --> Configuration Manager setup includes a prerequisite check to verify this configuration when creating a database through install or recovery.

    > [!NOTE]
    > When setup creates the database, and you configure **automatic** seeding, the availability group must have permissions to create the database. This requirement applies to both a new database or recovery. For more information, see [Automatic seeding for secondary replica](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### Replica member location

Either host all replicas in an availability group on-premises, or host them all on Microsoft Azure. A group that includes an on-premises member and a member in Azure isn't supported.

> [!NOTE]
> If you're using an Azure virtual machine for the SQL Server, enable **floating IP**. For more information, see [Configure a load balancer for a SQL Server Always On availability group in Azure virtual machines](/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure).<!-- SCCMDocs#1928 -->

Configuration Manager setup needs to connect to each replica. When you set up an availability group in Azure, and the group is behind an internal or external load balancer, open the following default ports:

- RPC Endpoint Mapper: **TCP 135**

- SQL Server Service Broker: **TCP 4022**

- SQL over TCP: **TCP 1433**

After setup completes, these ports must stay open for Configuration Manager and replication link analyzer.<!-- MEMDocs#375 -->

You can use custom ports for these configurations. Use the same custom ports by the endpoint and on all replicas in the availability group.

For SQL Server to replicate data between sites, create a load-balancing rule for each port in the Azure load balancer. For more information, see [Configure High Availability Ports for an internal load balancer](/azure/load-balancer/load-balancer-configure-ha-ports).<!-- MEMDocs#252 -->

#### Listener

The availability group must have at least one *availability group listener*. When you configure Configuration Manager to use the site database in the availability group, it uses the virtual name of this listener. Although an availability group can contain multiple listeners, Configuration Manager can only make use of one. For more information, see [Create or configure a SQL Server availability group listener](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### File paths

When you run Configuration Manager setup to configure a site to use the database in an availability group, each secondary replica server must have a SQL Server file path that's identical to the file path for the site database files on the current primary replica. If an identical path doesn't exist, setup fails to add the instance for the availability group as the new location of the site database.

The local SQL Server service account must have **Full Control** permission to this folder.

The secondary replica servers only require this file path while you're using Configuration Manager setup to specify the database instance in the availability group. After it completes configuration of the site database in the availability group, you can delete the unused path from secondary replica severs.

For example, consider the following scenario:

- You create an availability group that uses three SQL Servers.

- Your primary replica server is a new installation of SQL Server 2014. By default, it stores the database MDF and LDF files in `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.

- You upgraded both of your secondary replica servers to SQL Server 2014 from previous versions. With the upgrade, these servers keep the original file path to store database files: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.

- Before moving the site database to this availability group, on each secondary replica server, create the following file path: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. This path is a duplicate of the path in use on the primary replica, even if the secondary replicas won't use this file location.

- You then grant the SQL Server service account on each secondary replica full control access to the newly created file location on that server.

- You can now successfully run Configuration Manager setup to configure the site to use the site database in the availability group.

#### Multi-subnet failover

<!-- SCCMDocs-pr#3734 -->
You can enable the [MultiSubnetFailover connection string keyword](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) in SQL Server. You also need to manually add the following values to the Windows Registry on the site server:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!WARNING]
> Use of [site server high availability](site-server-high-availability.md) and SQL Server Always On availability groups with multi-subnet failover doesn't provide the full capabilities of automatic failover for disaster recovery scenarios.

If you need to create an availability group with a member in a remote location, prioritize based on the lowest network latency. High network latency can cause replication failures.<!-- SCCMDocs#1381 -->

## Limitations and known issues

The following limitations apply to all scenarios.

### Unsupported SQL Server options and configurations

- **Basic availability groups**: Introduced with SQL Server 2016 Standard edition, basic availability groups don't support read access to secondary replicas. Configuration requires this access. For more information, see [Basic SQL Server availability groups](/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups).

- **Failover cluster instance**: Failover cluster instances aren't supported for a replica you use with Configuration Manager. For more information, see [SQL Server Always On failover cluster instances](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).

### SQL Servers that host additional availability groups

<!--SCCMDocs issue 649-->
When the SQL Server hosts one or more availability groups in addition to the group you use for Configuration Manager, it needs specific settings at the time you run Configuration Manager setup. These settings are also needed to install an update for Configuration Manager. Each replica in each availability group must have the following configurations:

- Manual failover

- Allow any read-only connection

> [!NOTE]
> Configuration Manager supports using the availability group synchronous replicas when set to **Automatic Failover**. Set **Manual Failover** when:
>
> - You run Configuration Manager setup to specify use of the site database in the availability group.
> - You install any update to Configuration Manager. (Not just updates that apply to the site database).

### Unsupported database use

#### Configuration Manager supports only the site database in an availability group

The following databases aren't supported by Configuration Manager in an availability group:

- Reporting database

- WSUS database

#### Pre-existing database

You can't use a new database created on the replica. When you configure an availability group, restore a copy of an existing Configuration Manager database to the primary replica.

### Setup errors in ConfigMgrSetup.log

When you run Configuration Manager setup to move a site database to an availability group, it tries to process database roles on the secondary replicas of the availability group. The **ConfigMgrSetup.log** file shows the following error:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

These errors are safe to ignore.

### Site expansion

<!--SCCMDocs issue 568-->
If you configure the site database for a standalone primary site to use an availability group, you can't expand the site to include a central administration site. If you try this process, it fails. To expand the site, temporarily remove the primary site database from the availability group.

You don't need to make any changes to the configuration when adding a secondary site.

## Changes for site backup

### Backup database files

When a site database uses an availability group, run the built-in **Backup Site server** maintenance task to back up common Configuration Manager settings and files. Don't use the MDF or LDF files created by that backup. Instead, make direct backups of these database files by using SQL Server.

You can still use the SQL Server back up, however you can't restore it directly to a SQL Server Always On cluster. You need to restore it on a standalone server and move it back to SQL Server Always On.

### Transaction log

Set the recovery model of the site database to **Full**. This configuration is a requirement for Configuration Manager use in an availability group. Plan to monitor and maintain the size of the site database transaction log. In the full recovery model, the transactions aren't hardened until it makes a full backup of the database or transaction log. For more information, see [Back up and restore of SQL Server databases](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).

## Changes for site recovery

If at least one node of the availability group is still functional, use the site recovery option to **Skip database recovery (Use this option if the site database was unaffected)**.

Site recovery can recreate the database in an availability group. This process works with both manual and automatic seeding.<!-- SCCMDocs-pr#3846 -->

> [!TIP]
> When you run the setup/recovery wizard, the **New Availability Group Database** page only applies to manual seeding configurations. With automatic seeding, there's no shared database backup, so that page of the wizard isn't shown.<!-- SCCMDocs #2242 -->

For more information, see [Backup and recovery](../../manage/backup-and-recovery.md).

## Changes for reporting

### Install the reporting service point

The reporting services point doesn't support using the listener virtual name of the availability group. It also doesn't support hosting its database in an availability group.

- By default, the reporting services point installation sets the **Site database server name** to the virtual name that's specified as the listener. Change this setting to specify a computer name and instance of a replica in the availability group.

- To offload reporting and to increase availability when a replica node is offline, consider installing additional reporting services points on each replica node. Then configure each reporting services point to use its own computer name. When you install a reporting service point on each replica of the availability group, reporting can always connect to an active reporting point server.

### Switch the reporting services point used by the console

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Reporting**, and select the **Reports** node.

1. In the ribbon, select **Report Options**.

1. In the Report Options dialog box, select the reporting services point you want to use.

## Next steps

This article describes the prerequisites, limitations, and changes to common tasks that Configuration Manager requires when you use availability groups. For procedures to set up and configure your site to use availability groups, see [Configure availability groups](configure-aoag.md).
