---
title: Prerequisite checks
titleSuffix: Configuration Manager
description: Reference of the specific prerequisite checks for Configuration Manager updates.
ms.date: 03/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
---

# List of prerequisite checks for Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article details the prerequisite checks that run when you install or update Configuration Manager. For more information, see [Prerequisite checker](/sccm/core/servers/deploy/install/prerequisite-checker).  



## Errors

### Active migration mappings on the target primary site

*Applies to: Central administration site*

There are no active migration mappings to primary sites.

### Active replica MP

*Applies to: Primary site*

There's an active management point replica.

### Administrative rights on expand primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the user account that runs setup has **Administrator** rights on the standalone primary site server.

### Administrative rights on site system

*Applies to: Central administration site, primary site, secondary site*

The user account that runs Configuration Manager setup has **Administrator** rights on the site server.

### Administrator rights on central administration site

*Applies to: Primary site*

The user account that runs Configuration Manager setup has **Administrator** rights on the central administration site server.

### Asset Intelligence synchronization point on the expanded primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the Asset Intelligence synchronization point role isn't installed on the standalone primary site.

### BITS enabled

*Applies to: Management point*

Background Intelligent Transfer Service (BITS) is installed on the management point. This check can fail for one of the following reasons:

- BITS isn't installed  

- The IIS 6.0 WMI compatibility component for IIS 7.0 isn't installed on the server or remote IIS host  

- Setup was unable to verify remote IIS settings. IIS common components aren't installed on the site server.  

### Case-insensitive collation on SQL Server

*Applies to: Site database server*

The SQL Server installation uses a case-insensitive collation, such as **SQL_Latin1_General_CP1_CI_AS**.

### Central administration site server administrative rights on expand primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the computer account of the central administration site server has **Administrator** rights on the standalone primary site server.

### Client version on management point computer

*Applies to: Management point*

You're installing the management point on a server that doesn't have a different version of the Configuration Manager client installed.

### Cloud management gateway on the expanded primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the cloud management gateway role isn't installed on the standalone primary site.

### Connection to SQL Server on central administration site

*Applies to: Primary site*

The user account that runs Configuration Manager setup on the primary site to join an existing hierarchy has the **sysadmin** role on the SQL Server instance for the central administration site.

### Custom client agent settings have NAP enabled

*Applies to: Central administration site, primary site*

There are no custom client settings that enable network access protection (NAP).

### Data warehouse service point on the expanded primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the data warehouse service point role isn't installed on the standalone primary site.

### Dedicated SQL Server instance

*Applies to: Central administration site, primary site, secondary site*

You configured a dedicated instance of SQL Server to host the Configuration Manager site database.

If another site uses the instance, you must select a different instance for the new site. You can also uninstall the other site, or move its database to a different instance for the SQL server.

### Default client agent settings have NAP enabled

*Applies to: Central administration site, primary site*

The default client settings don't enable network access protection (NAP).

### Domain membership (error)

*Applies to: Central administration site, primary site, secondary site, SMS Provider, SQL Server*

The Configuration Manager computer is a member of a Windows domain.

### Endpoint Protection point on the expanded primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the Endpoint Protection point role isn't installed on the standalone primary site.

### Existing Configuration Manager server components on server

*Applies to: Central administration site, primary site, secondary site*

A site server or site system role isn't already installed on the server selected for site installation.

### Existing stand-alone primary site for version and site code

*Applies to: Central administration site, primary site*

The primary site you plan to expand is a standalone primary site. It has the same version of Configuration Manager, but a different site code than the central administration site to be installed.

### Firewall exception for SQL Server

*Applies to: Central administration site, primary site, secondary site, management point*

The Windows Firewall is disabled or a relevant Windows Firewall exception exists for SQL Server.

Allow Sqlservr.exe or the required TCP ports to be accessed remotely. By default, SQL Server listens on TCP port 1433, and the SQL Server Service Broker (SSB) uses TCP port 4022.

### Free disk space on site server

*Applies to: Central administration site, primary site, secondary site*

To install the site server, it must have at least 15 GB of free disk space. If you install the SMS Provider on the same server, it needs an additional 1 GB of free space.

### IIS service running

*Applies to: Management point, distribution point*

IIS is installed and running on the server for the management point or distribution point.

### Incompatible collection references

*Applies to: Central administration site*

During an upgrade, collections reference only other collections of the same type.

### Match collation of expand primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the site database for the standalone primary site has the same collation as the site database at the central administration site.

### Maximum text replication size for SQL Server Always On availability groups

*Applies to: Site database server*

When using SQL Server Always On, the **max text repl size** setting must be properly configured. For more information, see [Prepare to use SQL Server Always On availability groups with Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### Microsoft Intune Connector on the expanded primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the Microsoft Intune Connector role isn't installed on the standalone primary site.

### Microsoft Remote Differential Compression (RDC) library registered

*Applies to: Central administration site, primary site, secondary site*

The RDC library is registered on the Configuration Manager site server.

### Microsoft Windows Installer

*Applies to: Central administration site, primary site, secondary site*

Verifies the Windows Installer version.

When this check fails, setup wasn't able to verify the version, or the installed version doesn't meet the minimum requirement of Windows Installer 4.5.

### Minimum .NET Framework version for Configuration Manager console

*Applies to: Configuration Manager console*

Microsoft .NET Framework 4.0 is installed on the Configuration Manager console computer.

### Minimum .NET Framework version for Configuration Manager site server

*Applies to: Central administration site, primary site, secondary site*

.NET Framework 3.5 is installed or enabled on the Configuration Manager site server.

### Minimum .NET Framework version for SQL Server Express edition installation for Configuration Manager secondary site

*Applies to: Secondary site*

.NET Framework 4.0 is installed or enabled on the Configuration Manager secondary site server. This version is required by SQL Server Express.

### Parent database collation

*Applies to: Primary site, secondary site*

The collation of the site database matches the collation of the parent site's database. All sites in a hierarchy must use the same database collation.

### Parent site replication status

*Applies to: Central administration site, primary site*

The replication status of the parent site is **Replication active** (state **125**).

### Pending system restart

*Applies to: Central administration site, primary site, secondary site*

Before you run setup, another program requires the server to be restarted.

Starting in version 1810, this check is more resilient. To see if the computer is in a pending restart state, it checks the following registry locations:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### Primary FQDN

*Applies to: Central administration site, primary site, secondary site, site database server*

The NetBIOS name of the computer matches the local hostname in the fully qualified domain name (FQDN).

### Read-only domain controller

*Applies to: Central administration site, primary site, secondary site*

Site database servers and secondary site servers aren't supported on a read-only domain controller (RODC).

For more information, see the Microsoft Support article on [Problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911).

### Required SQL Server collation

*Applies to: Central administration site, primary site, secondary site*

The instance for SQL Server is configured to use the **SQL_Latin1_General_CP1_CI_AS** collation.

If the Configuration Manager site database is already installed, this check also applies to the database. For information about changing your SQL Server instance and database collations, see [SQL collation and unicode support](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support).

If you're using a Chinese OS and require GB18030 support, this check doesn't apply. For more information about enabling GB18030 support, see [International support](/sccm/core/plan-design/hierarchy/international-support).

### Server service is running

*Applies to: Central administration site, primary site, secondary site*

The Server service is started and running.

### Setup source folder

*Applies to: Secondary site*

The computer account for the secondary site has the following permissions to the setup source folder and share:

- **Read** NTFS file system permissions  

- **Read** share permissions  

> [!Note]  
> If you use administrative shares, for example, C$ and D$, the secondary site computer account must be an **Administrator** on the server.  

### Setup source version

*Applies to: Secondary site*

The Configuration Manager version in the specified source folder for the secondary site installation matches the Configuration Manager version of the primary site.

### Site code in use

*Applies to: Primary site*

The specified site code isn't already in use in the Configuration Manager hierarchy. Specify a unique site code for this site.

### Site server computer account administrative rights

*Applies to: Primary site, site database server*

The site server computer account has **Administrator** rights on the SQL server and management point.

### Site server FQDN length

*Applies to: Central administration site, primary site, secondary site*

The length of the FQDN of the site server.

### Site server in passive mode on the expanded primary site

*Applies to: Central administration site*

When you expand a primary site to a hierarchy, the site server in passive mode role isn't installed on the standalone primary site.

### SMS Provider in same domain as site server

*Applies to: SMS Provider*

Any instance of the SMS Provider is in the same domain as the site server.

### Software update point in NLB configuration

*Applies to: Software update point*

The site isn't using network load balancing (NLB) with any virtual locations for active software update points.

### Software update point using a load balancer

*Applies to: Software update point*

Configuration Manager doesn't support software update points on network (NLB) or hardware load balancers (HLB).

### SQL Server Always On availability groups

*Applies to: Site database server*

When using SQL Server Always On, it must meet the minimum requirements to host an availability group. For more information, see [Prepare to use SQL Server Always On availability groups with Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### SQL Server availability group configured for readable secondaries

*Applies to: Site database server*

When using SQL Server Always On, check the secondary read state of availability group replicas.

### SQL Server availability group configured for manual failover

*Applies to: Site database server*

When using SQL Server Always On, availability group replicas are configured for manual failover.

### SQL Server availability group replicas on default instance

*Applies to: Site database server*

When using SQL Server Always On, availability group replicas are on the default instance.

### SQL availability group replicas must all have the same seeding mode

<!-- SCCMDocs-pr#3899 -->
*Applies to: Site database server*

Starting in version 1906, when using SQL Server Always On, you need to configure availability group replicas with the same [seeding mode](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).

### SQL availability group replicas must be healthy

<!-- SCCMDocs-pr#3899 -->
*Applies to: Site database server*

Starting in version 1906, when using SQL Server Always On, availability group replicas are in a healthy state.

### SQL Server configuration for site upgrade

*Applies to: Site database server*

The SQL Server meets the minimum requirements for site upgrade. For more information, see [Supported SQL Server versions](/sccm/core/plan-design/configs/support-for-sql-server-versions).

### SQL Server edition

*Applies to: Site database server*

SQL Server at the site isn't SQL Server Express.

### SQL Server Express on secondary site

*Applies to: Secondary site*

SQL Server Express can successfully install on the secondary site server.

### SQL Server on the secondary site server

*Applies to: Secondary site*

SQL Server is installed on the secondary site server. You can't install SQL Server on a remote site system for a secondary site.

> [!Warning]  
> This check only applies when you select to have setup use an existing instance of SQL Server.  

### SQL Server service running account

*Applies to: Central administration site, primary site, secondary site*

The sign-in account for the SQL Server service isn't a local user account or **LOCAL SERVICE**.

Configure the SQL Server service to use a valid domain account, **NETWORK SERVICE**, or **LOCAL SYSTEM**.

### SQL Server site database consistency

*Applies to: Site database server*

Verify database consistency.

### SQL Server sysadmin rights

*Applies to: Site database server*

The user account that runs Configuration Manager setup has the **sysadmin** role on the SQL Server instance that you selected for site database installation. This check also fails when setup is unable to access the instance for the SQL Server to verify permissions.

### SQL Server sysadmin rights for reference site

*Applies to: Site database server*

The user account that runs Configuration Manager setup has the **sysadmin** role on the SQL Server role instance that you selected as the reference site database. SQL Server **sysadmin** role permissions are required to modify the site database.

### SQL Server TCP port

*Applies to: Site database server*

TCP is enabled for the SQL Server instance, and is set to use a static port.

### SQL Server version

*Applies to: Site database server*

A supported version of SQL Server is installed on the specified site database server.

For more information, see [Support for SQL Server versions](/sccm/core/plan-design/configs/support-for-sql-server-versions).

### Unsupported OS for Configuration Manager console

*Applies to: Configuration Manager console*

Install the Configuration Manager console on computers that run a supported OS version.

For more information, see the [Supported OS versions for the Configuration Manager console](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

### Unsupported OS for site server

*Applies to: Central administration site, primary site, secondary site, Configuration Manager console, management point, distribution point*

The server runs a supported OS version.

For more information, see [Supported OS versions for Configuration Manager site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

### Unsupported site system role: out of band service point

*Applies to: Primary site*

The out of band service point site system role isn't installed.

### Unsupported site system role: system health validation point

*Applies to: Primary site*

The system health validation point site system role isn't installed.

### Unsupported upgrade path

*Applies to: Central administration site, primary site*

All site servers in the hierarchy meet the Configuration Manager minimum version that's required for upgrade.

### USMT installed

*Applies to: Central administration site, primary site (standalone only)*

The User State Migration Tool (USMT) component of the Windows Assessment and Deployment Kit (ADK) for Windows is installed.

### Validate FQDN of SQL Server

*Applies to: Site database server*

You specified a valid FQDN for the SQL Server computer.

### Verify central administration site version

*Applies to: Primary site*

The central administration site has the same version of Configuration Manager.

### Verify database consistency

*Applies to: Central administration site, primary site*

Verifies consistency of the site database in SQL Server.  

### Windows Deployment Tools installed

*Applies to: SMS Provider*

The Windows Deployment Tools component of the Windows ADK is installed.

### Windows Failover Cluster

*Applies to: Site server, management point, distribution point*

Server with the site server, management point, or distribution point roles aren't part of a Windows Cluster.

Starting in version 1810, the Configuration Manager setup process no longer blocks installation of the site server role on a computer with the Windows role for Failover Clustering. SQL Always On requires this role, so previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using SQL Always On and a site server in passive mode. For more information, see [High availability options](/sccm/core/servers/deploy/configure/high-availability-options). <!--1359132-->  

### Windows PE installed

*Applies to: SMS Provider*

The Windows Preinstallation Environment (PE) component of the Windows ADK is installed.



## Warnings

### Active Directory domain functional level

*Applies to: Central administration site, primary site*

The Active Directory domain and forest functional level is a minimum of Windows Server 2008 R2. For more information, see [Support for Active Directory domains](/sccm/core/plan-design/configs/support-for-active-directory-domains).

### Administrative rights on distribution point

*Applies to: Distribution point*

The user account running setup has **Administrator** rights on the distribution point.

### Administrative rights on management point

*Applies to: Management point, distribution point*

The computer account of the site server has **Administrator** rights on the management point and distribution point.

### Administrative share (site system)

*Applies to: Management point*

The required administrative shares are present on the site system computer.

### Application compatibility

*Applies to: Central administration site, primary site*

Current applications are compliant with the application schema.

### Backlogged inboxes

*Applies to: Central administration site, primary site*

The site server is processing critical inboxes in a timely fashion. Inboxes don't contain files older than one day.

It checks the following inbox folders:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

To resolve this warning, check whether the despooler and scheduler site system components are running.

### BITS installed

*Applies to: Management point*

The Background Intelligent Transfer Service (BITS) is installed and enabled in IIS.

### Check if the site uses Upgrade Readiness cloud service connector

*Applies to: Central administration site, primary site*

The Upgrade Readiness service is retired as of January 31, 2020. For more information, see [KB 4521815: Windows Analytics retirement on January 31, 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Desktop Analytics is the evolution of Windows Analytics. For more information, see [What is Desktop Analytics](/sccm/desktop-analytics/overview).

If your Configuration Manager site had a connection to Upgrade Readiness, you need to remove it and reconfigure clients. For more information, see [Remove Upgrade Readiness connection](/configmgr/core/clients/manage/upgrade-readiness#bkmk_remove).

If you ignore this prerequisite warning, Configuration Manager setup automatically removes the Upgrade Readiness connector.<!-- #4898 -->

### Cloud management gateway requires either token-based authentication or an HTTPS management point

*Applies to: Cloud management gateway*

With some versions of Configuration Manager, you can't use an HTTP management point with the cloud management gateway (CMG). Either configure the CMG for HTTPS, or configure the site for enhanced HTTP. For more information, see [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

### Configuration for SQL Server memory usage

*Applies to: Site database server*

SQL Server is configured for unlimited memory use. Configure SQL Server memory to have a maximum limit.

### Distribution point package version

*Applies to: Distribution points*

All distribution points in the site have the latest version of software distribution packages.

### Domain membership (warning)

*Applies to: Management point, distribution point*

The Configuration Manager computer is a member of a Windows domain.

### Firewall exception for SQL Server (standalone primary site)

*Applies to: Primary site (standalone only)*

The Windows Firewall is disabled, or a relevant Windows Firewall exception exists for SQL Server.

Allow Sqlservr.exe or the required TCP ports to be accessed remotely. By default, SQL Server listens on TCP port 1433, and the Server Service Broker (SSB) uses TCP port 4022.

### Firewall exception for SQL Server for management point

*Applies to: Management point*

The Windows Firewall is disabled, or a relevant Windows Firewall exception exists for SQL Server.

### IIS HTTPS configuration

*Applies to: Management point, distribution point*

IIS website has bindings for the HTTPS communication protocol.

When you install site roles that require HTTPS, configure IIS site bindings on the specified server with a valid public key infrastructure (PKI) certificate.

### Invalid discovery records

*Applies to: central administration site*

There are discovery records that are no longer valid. These records will be marked for deletion.

### Microsoft XML Core Services 6.0 (MSXML60)

*Applies to Central administration site, primary site, secondary site, Configuration Manager console, management point, distribution point*

Verifies that MSXML 6.0 or a later version is installed.

### Network access protection (NAP) is no longer supported

*Applies to: Primary site*

There are no software updates that are enabled for NAP.

### NTFS drive on site server

*Applies to: Primary site*

The disk drive is formatted with the NTFS file system. For better security, install site server components on disk drives formatted with the NTFS file system.

### <a name="bkmk_pending-policy"></a> Pending configuration item policy updates

<!--SCCMDocs-pr issue 2814-->

*Applies to: Primary site*

Starting in version 1806, if you're updating from version 1706 or later, you may see this warning if you have many application deployments and at least one of them requires approval.

You have two options:  

- Ignore the warning and continue with the update. This action causes higher processing on the site server during the update as it processes the policies. You may also see more processor load on the management point after the update.  

- Revise one of the applications that has no requirements or a specific OS requirement. Pre-process some of the load on the site server at that time. Review **objreplmgr.log**, and then monitor the processor on the management point. After the processing is complete, update the site. There will still be some additional processing after the update, but less than if you ignore the warning with the first option.  

### Pending system restart on the remote SQL Server

*Applies to: Version 1902 and later, remote SQL Server*

Before you run setup, another program requires the server to be restarted.

To see if the computer is in a pending restart state, it checks the following registry locations:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### PowerShell 2.0 on site server

*Applies to: Primary site with Exchange connector*

Windows PowerShell 2.0 or a later version is installed on the site server for the Configuration Manager Exchange Connector.

### Remote connection to WMI on secondary site

*Applies to: Secondary site*

Setup can establish a remote connection to WMI on the secondary site server.

### Schema extensions

*Applies to: Central administration site, primary site*

The Active Directory schema has been extended. If it's extended, the version of the schema extensions that were used.

Configuration Manager doesn't require Active Directory schema extensions for site server installation. Microsoft recommends them for the full use of all Configuration Manager features. For more information about the advantages of extending the schema, see [Prepare Active Directory for site publishing](/sccm/core/plan-design/network/extend-the-active-directory-schema).

### Share name in package

*Applies to: Central administration site, primary site*

Packages don't have invalid characters in the share name, such as `#`.

### Site system to SQL Server communication

*Applies to: Secondary site, management point*

The account that you configured to run the SQL Server service for the site database instance has a valid service principal name (SPN) in Active Directory Domain Services. Register a valid SPN in Active Directory to support Kerberos authentication.

### <a name="bkmk_changetracking"></a> SQL Server change tracking cleanup

*Applies to: Site database server*

Starting in version 1810, check if the site database has a backlog of SQL change tracking data.<!--SCCMDocs-pr issue 3023-->  

Manually verify this check by running a diagnostic stored procedure in the site database. First, create a [diagnostic connection](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) to your site database. The easiest method is to use SQL Server Management Studio's Database Engine Query Editor, and connect to `admin:<instance name>`.

In a dedicated administrator connection query window, run the following commands:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Depending upon the size of your database and the backlog size, this stored procedure could run in a few minutes or several hours. When the query completes, you see two sections of data related to the backlog. First look at **CT_Days_Old**. This value tells you the age (days) of the oldest entry in your syscommittab table. It should be five days, which is the Configuration Manager default value. Don't change this default value. At times of heavy data processing or replication, the oldest entry in syscommittab could be over five days. If this value is above seven days, run a manual cleanup of change tracking data.  

To clean up the change tracking data, run the following command in the dedicated administration connection:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

This command starts a cleanup of syscommittab and all of the associated side tables. It can run in several minutes or several hours. To monitor its progress, query the **vLogs** view. To see the current progress, run the following query:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

When you install a new site, Configuration Manager automatically installs SQL Server Native Client as a redistributable component. After the site is installed, Configuration Manager doesn't upgrade SQL Server Native Client. Updating the SQL Server Native Client may require a restart, which can impact the site install process.

This check makes sure the site has a supported version of the SQL Native Client. Starting in version 1810, the minimum version is SQL 2012 SP4 (`11.*.7001.0`).

This SQL Native Client version supports TLS 1.2. For more information, see the following articles:

- [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [How to enable TLS 1.2 for Configuration Manager](/sccm/core/plan-design/security/enable-tls-1-2)  

Configuration Manager uses SQL Server Native Client on the following site system roles:<!-- SCCMDocs issue 1150 -->

- Site database server
- Site server: central administration site, primary site, or secondary site
- Management point
- Device management point
- State migration point
- SMS Provider
- Software update point
- Multicast-enabled distribution point
- Asset Intelligence update service point
- Reporting services point
- Application catalog web service
- Enrollment point
- Endpoint Protection point
- Service connection point
- Certificate registration point
- Data warehouse service point

### SQL Server process memory allocation

*Applies to: Site database server*

SQL Server reserves a minimum of 8 GB of memory for the central administration site and primary site, and a minimum of 4 GB of memory for the secondary site.

For more information, see [How to configure memory options using SQL Server Management Studio](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> This check isn't applicable to SQL Server Express on a secondary site. This edition is limited to 1 GB of reserved memory.  

### SQL Server security mode

*Applies to: Site database server*

SQL Server is configured for Windows authentication security.

### Unsupported site system OS version for upgrade

*Applies to: Primary site, secondary site*

Site system roles other than distribution points are installed on servers running Windows Server 2012 or later.

For more information, see [Supported operating systems for Configuration Manager site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

> [!NOTE]  
> This check can't resolve the status of site system roles installed in Azure or for the cloud storage used by Microsoft Intune. Ignore warnings for these roles as false positives.

### Upgrade Assessment Toolkit is unsupported

*Applies to: Central administration site, primary site*

The Upgrade Assessment Toolkit isn't installed. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

### Verify site server permissions to publish to Active Directory

*Applies to: Central administration site, primary site, secondary site*

The computer account for the site server has **Full Control** permissions to the **System Management** container in the Active Directory domain.

For more information, see [Prepare Active Directory for site publishing](/sccm/core/plan-design/network/extend-the-active-directory-schema).

> [!NOTE]  
> If you manually verify the permissions, you can ignore this warning.

### Windows Remote Management (WinRM) v1.1

*Applies to: Primary site, Configuration Manager console*

WinRM 1.1 is installed on the primary site server or the Configuration Manager console computer to run the out-of-band management console.

WinRM is automatically installed with all currently-supported versions of Windows. For more information, see [Installation and configuration for Windows Remote Management](https://docs.microsoft.com/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### WSUS on site server

*Applies to: Central administration site, primary site*

A supported version of Windows Server Update Services (WSUS) is installed on the site server.

When you use a software update point on a server other than the site server, you must install the WSUS Administration Console on the site server. For more information about WSUS, see [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).
