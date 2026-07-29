---
title: Supported SQL Server versions
description: Learn which SQL Server versions, editions, and compatibility levels Configuration Manager supports.
ms.date: 07/28/2026
ms.subservice: core-infrastructure
ms.topic: reference
ms.collection: tier3
ms.service: microsoft-endpoint-configuration-manager
---

# Supported SQL Server versions for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Each Configuration Manager site requires a supported SQL Server version to host the site database. For required and optional settings, see [Supported configurations for SQL Server](supported-configurations-for-sql-server.md).

## <a name="bkmk_Instances"></a> SQL Server instances and locations

### SQL Server features

Only the **Database Engine Services** feature is required for each site server.

Configuration Manager database replication doesn't require the **SQL Server replication** feature. However, this SQL Server configuration is required when you use [database replicas for management points](../../servers/deploy/configure/database-replicas-for-management-points.md).

### SQL Server instance

Use a dedicated instance of SQL Server for each site. The instance can be a **named instance** or the **default instance**.

### Central administration site and primary sites

The site database must use a full installation of SQL Server.

SQL Server can be located on:

- The site server computer.
- A computer that is remote from the site server.

The following instances are supported:

- The default or named instance of SQL Server.

- Multiple instance configurations.

- A SQL Server Always On failover cluster instance. For more information, see [Use a SQL Server Always On failover cluster instance for the site database](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

- A SQL Server Always On availability group. For more information, see [Prepare to use a SQL Server Always On availability group](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### Secondary sites

The site database can use the default instance of a full installation of SQL Server or SQL Server Express.

SQL Server must be located on the site server computer.

> [!IMPORTANT]
> Upgrade SQL 2012 or 2014 Express, Standard, Enterprise edition to SQl 2016 or latest version. Visual C++ Redistributable need to be upgraded to latest version on Secondary site: [Download Latest Microsoft Visual C++ Redistributable Version](https://aka.ms/vs/17/release/vc_redist.x64.exe).

### Data warehouse service point

The data warehouse uses a separate database. You can host it on the site database server, or a separate SQL Server. For more information, see [The data warehouse service point for Configuration Manager](../../servers/manage/data-warehouse.md).

### Limitations to support

The following configurations aren't supported:

- A failover cluster instance in a Network Load Balancing (NLB) cluster configuration

- A failover cluster instance on a Cluster Shared Volume (CSV)

- SQL Server database mirroring technology, and peer-to-peer replication

SQL Server transactional replication is supported only for replicating objects to management points that are configured to use [database replicas](../../servers/deploy/configure/database-replicas-for-management-points.md).

## <a name="bkmk_SQLVersions"></a> Supported versions of SQL Server

In a hierarchy with multiple sites, different sites can use different versions of SQL Server to host the site database. So long as the following items are true:

- Configuration Manager supports the versions of SQL Server that you use.
- The SQL Server versions you use remain in support by Microsoft.
- SQL Server supports replication between the two versions of SQL Server. For more information, see [SQL Server replication backward compatibility](/sql/relational-databases/replication/replication-backward-compatibility).

For SQL Server 2016 and prior, support for each SQL Server version and service pack follows the [Microsoft Lifecycle Policy](/lifecycle/products/?products=sql-server). Support for a specific SQL Server service pack includes cumulative updates unless they break backward compatibility to the base service pack version. Starting with SQL Server 2017, service packs won't be released since it follows a [modern servicing model](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server). The SQL Server team recommends ongoing, [proactive installation of cumulative updates](/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism) as they become available.

Unless specified otherwise, the following versions of SQL Server are supported with all active versions of Configuration Manager. If support for a new SQL Server version is added, the Configuration Manager version that adds that support is noted. Similarly, if support is deprecated, look for details about affected versions of Configuration Manager.

> [!IMPORTANT]
> When you use SQL Server Standard for the database at the central administration site, you limit the total number of clients that a hierarchy can support. See [Size and scale numbers](size-and-scale-numbers.md).

### SQL Server architecture

Configuration Manager requires a 64-bit version of SQL Server to host the site database.

### Standard / Enterprise SQL Editions

| SQL Version | Minimum Required Update | Supported Site Types | Notes |
|------------|-------------------------|--------------------------|-------|
| **SQL Server 2025** | RTM | CAS, Primary, Secondary | Support added in **version 2603**. CU must be supported by SQL lifecycle. |
| **SQL Server 2022** | RTM | CAS, Primary, Secondary | Support added in **version 2303**. Support for SQL 2022 Compatibility Level (160) added in **version 2603** <!--17536046-->. CU must be supported by SQL lifecycle. |
| **SQL Server 2019** | Cumulative Update 5 (CU5) or later | CAS, Primary, Secondary | CU5 is the minimum requirement as it resolves an issue with [scalar UDF inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining). CU must be supported by SQL lifecycle. |
| **SQL Server 2017** | Cumulative Update 2 (CU2) or later | CAS, Primary, Secondary | CU must be supported by SQL lifecycle. |
| **SQL Server 2016** | Minimum Service Pack supported by  [SQL 2016 lifecycle](/lifecycle/products/sql-server-2016) | CAS, Primary, Secondary |  |
| ~~**SQL Server 2014**~~ | Deprecated | CAS, Primary, Secondary | Deprecated in **version 2409**. SQL 2014 support ended July 2024. |

<!--### SQL Server 2014: Standard, Enterprise

You can use this version with the minimum service pack and cumulative update supported by the SQL Server lifecycle. You can use this version of SQL Server for the following sites:

- A central administration site
- A primary site
- A secondary site

<!--### SQL Server 2012: Standard, Enterprise

You can use this version with the minimum service pack and cumulative update supported by the SQL Server lifecycle. You can use this version of SQL Server for the following sites:

- A central administration site
- A primary site
- A secondary site

> [!IMPORTANT]
> Starting in version 2409, support for SQL Server 2014 is deprecated.<!--10092858--> 
> <!--Its support lifecycle ends in July 2024. Plan to upgrade all database servers before that time. For more information, see [SQL Server](../changes/deprecated/removed-and-deprecated-server.md#sql-server).-->
### Express Editions (Secondary Sites Only)

| SQL Version | Minimum Required Update | Supported Site Types | Notes |
|------------|-------------------------|--------------------------|-------|
| **SQL Server 2025 Express** | RTM | Secondary | Support added in **version 2603**. CU must be supported by SQL lifecycle. |
| **SQL Server 2022 Express** | RTM | Secondary | Shipped with version 2509. Support for SQL 2022 Compatibility Level (160) added in **version 2603**. |
| **SQL Server 2019 Express** | Cumulative Update 5 (CU5) or later | Secondary | CU5 is the minimum requirement as it resolves an issue with [scalar UDF inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining). CU must be supported by SQL lifecycle. |
| **SQL Server 2017 Express** | Cumulative Update 2 (CU2) or later | Secondary | CU must be supported by SQL lifecycle. |
| **SQL Server 2016 Express** | Minimum Service Pack supported by [SQL 2016 lifecycle](/lifecycle/products/sql-server-2016) | Secondary |  |
| ~~**SQL Server 2014 Express**~~ | Deprecated | Secondary | Deprecated in **version 2409**. SQL 2014 support ended July 2024.  |

<!--### SQL Server 2014 Express

You can use this version with the minimum service pack and cumulative update supported by the SQL Server lifecycle. You can use this version of SQL Server for the following sites:

- A secondary site

<!--### SQL Server 2012 Express

You can use this version with the minimum service pack and cumulative update supported by the SQL Server lifecycle. You can use this version of SQL Server for the following sites:

- A secondary site

> [!IMPORTANT]
> Starting in version 2409, support for SQL Server 2014 is deprecated.<!--10092858--> 
> <!--Its support lifecycle ends in July 2024. Plan to upgrade all database servers before that time. For more information, see [SQL Server](../changes/deprecated/removed-and-deprecated-server.md#sql-server).-->

## Database compatibility level

Configuration Manager requires that the compatibility level for the site database is no less than the lowest supported SQL Server version for your Configuration Manager version.

When you upgrade a site database from an earlier version of SQL Server, the database keeps its existing cardinality estimation level, if it's at the minimum allowed for that instance of SQL Server. When you upgrade SQL Server with a database at a compatibility level lower than the allowed level, it automatically sets the database to the lowest compatibility level allowed by SQL Server.

The following table identifies the recommended compatibility levels for Configuration Manager site databases:

|SQL Server version | Supported compatibility levels | Recommended level |
|----------------|--------------------|--------|
| SQL Server 2025  (since version 2603) | 170, 160, 150, 140, 130, 120, 110 | 170 |
| SQL Server 2022 | 160 (since version 2603), 150, 140, 130, 120, 110 | 150 |
| SQL Server 2019 | 150, 140, 130, 120, 110 | 150 |
| SQL Server 2017 | 140, 130, 120, 110 | 140 |
| SQL Server 2016 | 130, 120, 110 | 130 |
<!--| SQL Server 2014 | 120, 110 | 110 |-->

To identify the compatibility level in use for your site database, run the following SQL query on the site database server:

```SQL
SELECT name, compatibility_level FROM sys.databases
```

For more information on SQL Server compatibility levels and how to set them, see [ALTER DATABASE Compatibility Level (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).

## SQL Server Reporting Services

SQL Server Reporting Services is required for installing a reporting services point that lets you run reports. Configuration Manager supports the same versions of SQL Server for reporting as it does for the site database.

For more information, see [Prerequisites for reporting in Configuration Manager](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]
> After you upgrade SQL Server from a previous version, you might see the following error: *Report Builder Does Not Exist*.
> To resolve this error, you must reinstall the reporting services point site system role.

## Upgrade options for SQL Server

If you need to upgrade your version of SQL Server, use one of the following methods, from easy to more complex:

- [Upgrade SQL Server in-place](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (recommended)

- Install a new version of SQL Server on a new computer, and then [use the database move option](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) of Configuration Manager setup to point your site server to the new SQL Server

- Use [backup and recovery](../../servers/manage/backup-and-recovery.md). Using backup and recovery for a SQL Server upgrade scenario is supported. You can ignore the SQL Server versioning requirement when reviewing [Considerations before recovering a site](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site).
