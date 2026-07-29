---
title: Supported configurations for SQL Server
description: Learn about required and optional SQL Server and database configurations for Configuration Manager.
ms.date: 07/28/2026
ms.subservice: core-infrastructure
ms.topic: reference
ms.collection: tier3
ms.service: microsoft-endpoint-configuration-manager
---

# Supported configurations for SQL Server in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article identifies required and optional SQL Server configurations for Configuration Manager. For supported versions, editions, and compatibility levels, see [Supported SQL Server versions](support-for-sql-server-versions.md).

## <a name="bkmk_SQLConfig"></a> Required SQL Server instance configurations

The following configurations are required by all installations of SQL Server that you use for a site database, including SQL Server Express. When Configuration Manager installs SQL Server Express as part of a secondary site installation, it automatically creates these configurations.

### SQL Server instance and database collation

At each site, both the instance of SQL Server that's used for the site and the site database must use the following collation: **SQL_Latin1_General_CP1_CI_AS**.

Configuration Manager supports two exceptions to this collation for the China GB18030 standard. For more information, see [International support](../hierarchy/international-support.md).

### Windows authentication

Configuration Manager requires **Windows authentication** to validate connections to the database.

### Server memory configuration

Reserve memory for SQL Server by using SQL Server Management Studio. Set the **Minimum server memory** setting under **Server Memory Options**. For more information about how to configure this setting, see [SQL Server memory server configuration options](/sql/database-engine/configure-windows/server-memory-server-configuration-options).

- **For a database server that you install on the same computer as the site server**: Limit the memory for SQL Server to 50 to 80 percent of the available addressable system memory.

- **For a dedicated database server that's remote from the site server**: Limit the memory for SQL Server to 80 to 90 percent of the available addressable system memory.

- **For a memory reserve for the buffer pool of each SQL Server instance in use**:

  - For a central administration site: Set a minimum of 8 GB.
  - For a primary site: Set a minimum of 8 GB.
  - For a secondary site: Set a minimum of 4 GB.

### Required server configuration options

Configuration Manager sets the below SQL Server instance configurations during setup to function correctly. They apply for both standalone primary site and hierarchy scenarios. Do not alter them unless instructed by Microsoft support.

| Display name | Canonical name | Required value | More information link |
|--------------|---------------|----------------|------------------|
| CLR integration | `clr enabled` | True | [Introduction to SQL Server CLR Integration](/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration). |
| Allow Triggers to Fire Others | `nested triggers` | True | [Configure the nested triggers server configuration option](/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option). |
| Max Text Replication Size | `max text repl size (B)` | 2147483647 | [Configure the max text repl size server configuration option](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option). |

## <a name="bkmk_DBConfig"></a> Required site database options

Configuration Manager sets the below database configurations during setup to function correctly. They apply for both standalone primary site and hierarchy scenarios - as well as for SQL Always On configurations.

Do not alter them unless instructed by Microsoft support. The [Support policies for manual database changes](/troubleshoot/mem/configmgr/setup-migrate-backup-recovery/support-policy-for-manual-database-changes) article applies for database options.

| Display name | Canonical name | Required value | More information link |
|--------------|---------------|----------------|------------------|
| Database owner | `owner_sid` | `sa` | [ALTER AUTHORIZATION for databases](/sql/t-sql/statements/alter-authorization-transact-sql#alter-authorization-for-databases) |
| Change tracking | `CHANGE_TRACKING` | True (ON) | [Enable change tracking](/sql/relational-databases/track-changes/about-change-tracking-sql-server) |
| Recursive Triggers Enabled | `RECURSIVE_TRIGGERS` | True (ON) | [Recursive Triggers](/sql/relational-databases/triggers/create-nested-triggers#recursive-triggers) |
| Broker Enabled | `ENABLE_BROKER` | True (ON) | [Activate Service Broker in a database](/sql/database-engine/service-broker/how-to-activate-service-broker-message-delivery-in-databases-transact-sql#activate-service-broker-in-a-database) |
| Honor Broker Priority | `HONOR_BROKER_PRIORITY` | True (ON) | [Enable conversation priorities](/sql/database-engine/service-broker/managing-conversation-priorities#enable-conversation-priorities) |
| Trustworthy | `TRUSTWORTHY` | True (ON) | [TRUSTWORTHY database property](/sql/relational-databases/security/trustworthy-database-property) |
| Allow Snapshot Isolation | `ALLOW_SNAPSHOT_ISOLATION` | True (ON) | [Snapshot Isolation in SQL Server](/dotnet/framework/data/adonet/sql/snapshot-isolation-in-sql-server) |
| Is Read Committed Snapshot On | `READ_COMMITTED_SNAPSHOT` | True (ON) | [Set Transaction Isolation Level](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql) |
| ANSI Nulls Enabled | `ANSI_NULLS` | True (ON) | [SET ANSI_NULLS](/sql/t-sql/statements/set-ansi-nulls-transact-sql) |
| ANSI Padding Enabled | `ANSI_PADDING` | True (ON) | [SET ANSI_PADDING](/sql/t-sql/statements/set-ansi-padding-transact-sql) |
| ANSI Warnings Enabled | `ANSI_WARNINGS` | True (ON) | [SET ANSI_WARNINGS](/sql/t-sql/statements/set-ansi-warnings-transact-sql) |
| Arithmetic Abort Enabled | `ARITHABORT` | True (ON) | [SET ARITHABORT](/sql/t-sql/statements/set-arithabort-transact-sql) |
| Concatenate Null Yields Null | `CONCAT_NULL_YIELDS_NULL` | True (ON) | [SET CONCAT_NULL_YIELDS_NULL](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql) |
| Quoted Identifiers Enabled | `QUOTED_IDENTIFIER` | True (ON) | [SET QUOTED_IDENTIFIER](/sql/t-sql/statements/set-quoted-identifier-transact-sql) |
| Numeric Round-abort | `NUMERIC_ROUNDABORT` | False (OFF) | [SET NUMERIC_ROUNDABORT](/sql/t-sql/statements/set-numeric-roundabort-transact-sql) |

## <a name="bkmk_optional"></a> Optional configurations

The following configurations are optional for each database that uses a full SQL Server installation.

### SQL Server service account

You can configure the SQL Server service to run using:

- A *low rights domain user* account:

  - This configuration is a best practice and might require you to manually register the service principal name (SPN) for the account.

- The **local system** account of the computer that runs SQL Server:

  - Use the local system account to simplify the configuration process.
  - When you use the local system account, Configuration Manager automatically registers the SPN for the SQL Server service.
  - Using the local system account for the SQL Server service isn't a SQL Server best practice.

When the computer running SQL Server doesn't use its local system account to run the SQL Server service, configure the SPN of the account that runs the SQL Server service in Active Directory Domain Services. (When the system account is used, the SPN is automatically registered for you.)

For information about SPNs for the site database, see [Manage the SPN for the site database server](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).

For information about how to change the account that is used by the SQL Server service, see [SCM Services - Change the service startup account](/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).

### Extended protection for authentication
<!--24501008-->

Starting from version 2603, Configuration Manager supports SQL extended protection for authentication. It's a security feature that enhances protection against MITM attacks, making SQL server more secure when connections are made using extended protection. These enhancements collectively reduce the risk of unauthorized access and protect sensitive data managed by the SQL Server database engine.

For more information, see [Connect to the Database Engine Using Extended Protection](/sql/database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection).

### Force encryption
<!--16590006-->

Starting from version 2603, Configuration Manager supports setting **Force Encryption** to **Yes** on the SQL Server instance. This setting requires all clients to encrypt connections to the Database Engine. It helps protect against man-in-the-middle (MITM) attacks and reduces the risk of unauthorized access to data in the site database.

For more information, see [Encrypt connections to SQL Server by importing a certificate](/sql/database-engine/configure-windows/configure-sql-server-encryption#step-2-configure-encryption-settings-in-sql-server).

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

For an example of how to configure SQL Server to use a specific port, see [Configure a server to listen on a specific TCP port](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).
