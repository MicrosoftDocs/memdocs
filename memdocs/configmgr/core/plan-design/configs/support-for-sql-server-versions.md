---
title: Supported SQL Server versions
titleSuffix: Configuration Manager
description: Get SQL Server version and configuration requirements for hosting a Configuration Manager site database.
ms.date: 04/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
---

# Supported SQL Server versions for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Each Configuration Manager site requires a supported SQL Server version and configuration to host the site database.  

## <a name="bkmk_Instances"></a> SQL Server instances and locations

### Central administration site and primary sites

The site database must use a full installation of SQL Server.  

SQL Server can be located on:  

- The site server computer.  
- A computer that is remote from the site server.  

The following instances are supported:  

- The default or named instance of SQL Server.  
- Multiple instance configurations.  
- A SQL Server cluster. See [Use a SQL Server cluster to host the site database](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- A SQL Server AlwaysOn availability group. For more information, see [SQL Server AlwaysOn for a highly available site database](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### Secondary sites

The site database can use the default instance of a full installation of SQL Server or SQL Server Express.  

SQL Server must be located on the site server computer.  

### Limitations to support

The following configurations aren't supported:

- A SQL Server cluster in a Network Load Balancing (NLB) cluster configuration
- A SQL Server cluster on a Cluster Shared Volume (CSV)
- SQL Server database mirroring technology, and peer-to-peer replication

SQL Server transactional replication is supported only for replicating objects to management points that are configured to use [database replicas](../../servers/deploy/configure/database-replicas-for-management-points.md).  

## <a name="bkmk_SQLVersions"></a> Supported versions of SQL Server

In a hierarchy with multiple sites, different sites can use different versions of SQL Server to host the site database. So long as the following items are true:

- Configuration Manager supports the versions of SQL Server that you use.
- The SQL Server versions you use remain in support by Microsoft.
- SQL Server supports replication between the two versions of SQL Server. For more information, see [SQL Server replication backward compatibility](https://docs.microsoft.com/sql/relational-databases/replication/replication-backward-compatibility).

For SQL Server 2016 and prior, support for each SQL version and service pack follows the [Microsoft Lifecycle Policy](https://aka.ms/sqllifecycle). Support for a specific SQL Server service pack includes cumulative updates unless they break backward compatibility to the base service pack version. Starting with SQL Server 2017, service packs won't be released since it follows a [modern servicing model](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server/). The SQL Server team recommends ongoing, [proactive installation of cumulative updates](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/) as they become available.

Unless specified otherwise, the following versions of SQL Server are supported with all active versions of Configuration Manager. If support for a new SQL Server version is added, the Configuration Manager version that adds that support is noted. Similarly, if support is deprecated, look for details about affected versions of Configuration Manager.

> [!IMPORTANT]  
> When you use SQL Server Standard for the database at the central administration site, you limit the total number of clients that a hierarchy can support. See [Size and scale numbers](size-and-scale-numbers.md).

### SQL Server 2019: Standard, Enterprise

Starting with Configuration Manager version 1910, you can use this version with any cumulative update, as long as your cumulative update version is supported by the SQL lifecycle.

This version of SQL can be used for the following sites:

- A central administration site
- A primary site
- A secondary site

#### Known issue with SQL Server 2019

There's a known issue<!--6436234--> with the new [scalar UDF inlining](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.

### SQL Server 2017: Standard, Enterprise

You can use this version with [cumulative update version 2](https://support.microsoft.com/help/4052574) or higher, as long as your cumulative update version is supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A central administration site  
- A primary site  
- A secondary site  
  <!--SMS.498506-->

### SQL Server 2016: Standard, Enterprise  
<!--514985-->
You can use this version with the minimum service pack and cumulative update supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A central administration site  
- A primary site  
- A secondary site  

### SQL Server 2014: Standard, Enterprise

You can use this version with the minimum service pack and cumulative update supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A central administration site  
- A primary site  
- A secondary site

### SQL Server 2012: Standard, Enterprise

You can use this version with the minimum service pack and cumulative update supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A central administration site  
- A primary site  
- A secondary site  

### SQL Server 2017 Express

You can use this version with [cumulative update version 2](https://support.microsoft.com/help/4052574) or higher, as long as your cumulative update version is supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A secondary site
<!--SMS.498506-->

### SQL Server 2016 Express

You can use this version with the minimum service pack and cumulative update supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A secondary site

### SQL Server 2014 Express

You can use this version with the minimum service pack and cumulative update supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A secondary site  

### SQL Server 2012 Express

You can use this version with the minimum service pack and cumulative update supported by the SQL lifecycle. This version of SQL can be used for the following sites:

- A secondary site  

## <a name="bkmk_SQLConfig"></a> Required configurations for SQL Server

The following configurations are required by all installations of SQL Server that you use for a site database, including SQL Server Express. When Configuration Manager installs SQL Server Express as part of a secondary site installation, it automatically creates these configurations.  

### SQL Server architecture version

Configuration Manager requires a 64-bit version of SQL Server to host the site database.  

### Database collation

At each site, both the instance of SQL Server that's used for the site and the site database must use the following collation: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager supports two exceptions to this collation for the China GB18030 standard. For more information, see [International support](../hierarchy/international-support.md).  

### Database compatibility level

Configuration Manager requires that the compatibility level for the site database is no less than the lowest supported SQL Server version for your Configuration Manager version. For instance, beginning with version 1702, you need to have a [database compatibility level](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) greater than or equal to 110. <!-- SMS.506266-->

### SQL Server features

Only the **Database Engine Services** feature is required for each site server.  

Configuration Manager database replication doesn't require the **SQL Server replication** feature. However, this SQL Server configuration is required when you use [database replicas for management points](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### Windows authentication

Configuration Manager requires **Windows authentication** to validate connections to the database.  

### SQL Server instance

Use a dedicated instance of SQL Server for each site. The instance can be a **named instance** or the **default instance**.  

### SQL Server memory

Reserve memory for SQL Server by using SQL Server Management Studio. Set the **Minimum server memory** setting under **Server Memory Options**. For more information about how to configure this setting, see [SQL Server memory server configuration options](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **For a database server that you install on the same computer as the site server**: Limit the memory for SQL Server to 50 to 80 percent of the available addressable system memory.  

- **For a dedicated database server that's remote from the site server**: Limit the memory for SQL Server to 80 to 90 percent of the available addressable system memory.  

- **For a memory reserve for the buffer pool of each SQL Server instance in use**:  

  - For a central administration site: Set a minimum of 8 GB.  
  - For a primary site: Set a minimum of 8 GB.  
  - For a secondary site: Set a minimum of 4 GB.  

### SQL nested triggers

SQL nested triggers must be enabled. For more information, see [Configure the nested triggers server configuration option](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)

### SQL Server CLR integration

The site database requires SQL Server common language runtime (CLR) to be enabled. This option is enabled automatically when Configuration Manager installs. For more information about CLR, see [Introduction to SQL Server CLR Integration](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### SQL Server Service Broker (SSB)

The SQL Server Service Broker is required both for intersite replication as well as for a single primary site.

### TRUSTWORTHY setting

Configuration Manager automatically enables the SQL [TRUSTWORTHY database property](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property). This property is required by Configuration Manager to be **ON**.

## <a name="bkmk_optional"></a> Optional configurations for SQL Server

The following configurations are optional for each database that uses a full SQL Server installation.  

### SQL Server service

You can configure the SQL Server service to run using:  

- A *low rights domain user* account:  

  - This configuration is a best practice and might require you to manually register the service principal name (SPN) for the account.  

- The **local system** account of the computer that runs SQL Server:  

  - Use the local system account to simplify the configuration process.  
  - When you use the local system account, Configuration Manager automatically registers the SPN for the SQL Server service.  
  - Using the local system account for the SQL Server service isn't a SQL Server best practice.  

When the computer running SQL Server doesn't use its local system account to run the SQL Server service, configure the SPN of the account that runs the SQL Server service in Active Directory Domain Services. (When the system account is used, the SPN is automatically registered for you.)

For information about SPNs for the site database, see [Manage the SPN for the site database server](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).  

For information about how to change the account that is used by the SQL Server service, see [SCM Services - Change the service startup account](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### SQL Server Reporting Services

SQL Server Reporting Services is required for installing a reporting services point that lets you run reports. Configuration Manager supports the same versions of SQL Server for reporting as it does for the site database.

For more information, see [Prerequisites for reporting in Configuration Manager](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]  
> After you upgrade SQL Server from a previous version, you might see the following error: *Report Builder Does Not Exist*.  
> To resolve this error, you must reinstall the reporting services point site system role.  

### Data warehouse service point

The data warehouse uses a separate database. You can host it on the site database server, or a separate SQL Server. For more information, see [The data warehouse service point for Configuration Manager](../../servers/manage/data-warehouse.md).

### SQL Server ports

For communication to the SQL Server database engine and for intersite replication, you can use the default SQL Server port configurations or specify custom ports:  

- **Intersite communications** use the SQL Server Service Broker, which uses port TCP 4022 by default.  
- **Intrasite communications** between the SQL Server database engine and various Configuration Manager site system roles use port TCP 1433 by default. The following site system roles communicate directly with the SQL Server database:  

  - Management point  
  - SMS Provider computer  
  - Reporting services point  
  - Site server  

When a computer running SQL Server hosts a database from more than one site, each database must use a separate instance of SQL Server. Also, each instance must be configured to use a unique set of ports.  

> [!WARNING]  
> Configuration Manager doesn't support dynamic ports. Because SQL Server named instances by default use dynamic ports for connections to the database engine, when you use a named instance, you must manually configure the static port that you want to use for intrasite communication.  

If you have a firewall enabled on the computer that is running SQL Server, make sure that it's configured to allow the ports that are being used by your deployment and at any locations on the network between computers that communicate with the SQL Server.  

For an example of how to configure SQL Server to use a specific port, see [Configure a server to listen on a specific TCP port](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## Upgrade options for SQL Server

If you need to upgrade your version of SQL Server, use one of the following methods, from easy to more complex:  

- [Upgrade SQL Server in-place](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (recommended)  

- Install a new version of SQL Server on a new computer, and then [use the database move option](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) of Configuration Manager setup to point your site server to the new SQL Server  

- Use [backup and recovery](../../servers/manage/backup-and-recovery.md). Using backup and recovery for a SQL upgrade scenario is supported. You can ignore the SQL versioning requirement when reviewing [Considerations before recovering a site](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site).
