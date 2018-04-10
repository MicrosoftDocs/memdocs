---
title: "Supported SQL Server versions"
titleSuffix: "Configuration Manager"
description: "Get SQL Server version and configuration requirements for hosting a System Center Configuration Manager site database."
ms.custom: na
ms.date: 02/14/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: mestew
ms.author: mstewart
manager: dougeby

---
# Supported SQL Server versions for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Each System Center Configuration Manager site requires a supported SQL Server version and configuration to host the site database.  

##  <a name="bkmk_Instances"></a> SQL Server instances and locations  
 **Central administration site and primary sites**  
 The site database must use a full installation of SQL Server.  

 SQL Server can be located on:  

-   The site server computer.  
-   A computer that is remote from the site server.  

The following instances are supported:  

-   The default or named instance of SQL Server.  
-   Multiple instance configurations.  
-   A SQL Server cluster. See [Use a SQL Server cluster to host the site database](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
-   A SQL Server AlwaysOn availability group. This option requires Configuration Manager version 1602 or later. For details, see [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).


 **Secondary sites**  
 The site database can use the default instance of a full installation of SQL Server or SQL Server Express.  

 SQL Server must be located on the site server computer.  

 **Limitations to support**   
 The following configurations are not supported:
 -   A SQL Server cluster in a Network Load Balancing (NLB) cluster configuration
 -   A SQL Server cluster on a Cluster Shared Volume (CSV)
 -   SQL Server database mirroring technology, and peer-to-peer replication

SQL Server transactional replication is supported only for replicating objects to management points that are configured to use [database replicas](https://technet.microsoft.com/library/mt608546.aspx).  

##  <a name="bkmk_SQLVersions"></a> Supported versions of SQL Server  
 In a hierarchy with multiple sites, different sites can use different versions of SQL Server to host the site database. So long as the following items are true:
 -  Configuration Manager supports the versions of SQL Server that you use.
 -  The SQL Server versions you use remain in support by Microsoft.
 -  SQL Server supports replication between the two versions of SQL Server.  For example, [SQL Server does not support replication between SQL Server 2008 R2 and SQL Server 2016](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication).



 Unless specified otherwise, the following versions of SQL Server are supported with all active versions of System Center Configuration Manager. If support for a new SQL Server version or service pack is added, the Configuration Manager version that adds that support is noted. Similarly, if support is deprecated, look for details about affected versions of Configuration Manager.   

Support for a specific SQL Server service pack includes cumulative updates unless they break backward compatibility to the base service pack version. When no service pack version is noted, support is for the version of SQL Server with no service pack. In the future, if a service pack is released for a SQL Server version, a separate support statement is declared before the new service pack version is supported.


> [!IMPORTANT]  
>  When you use SQL Server Standard for the database at the central administration site, you limit the total number of clients that a hierarchy can support. See [Size and scale numbers](../../../core/plan-design/configs/size-and-scale-numbers.md).

### SQL Server 2017: Standard, Enterprise  
You can use this version of SQL Server, with a minimum of [cumulative update version 2](https://support.microsoft.com/help/4052574), beginning with [Configuration Manager version 1710](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1710) for the following sites: 

-   A central administration site  
-   A primary site  
-   A secondary site  
<!--SMS.498506-->

### SQL Server 2016 SP1: Standard, Enterprise  
You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site  

### SQL Server 2016: Standard, Enterprise  
You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site  


### SQL Server 2014 SP2: Standard, Enterprise  
You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site

### SQL Server 2014 SP1: Standard, Enterprise  
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site

### SQL Server 2012 SP4: Standard, Enterprise  
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site  

### SQL Server 2012 SP3: Standard, Enterprise  
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site  

<!-- Support for this service pack version has been dropped by Microsoft    
### SQL Server 2012 SP2: Standard, Enterprise   
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site  
-->

### SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter     
  This version of SQL Server is not supported [beginning with version 1702.](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database)  
 This version of SQL Server remains supported when you use a version of Configuration Manager prior to 1702.

When supported by the Configuration Manager version, you can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site
-   A secondary site

### SQL Server 2017 Express   
You can use this version of SQL Server, with a minimum of [cumulative update version 2](https://support.microsoft.com/help/4052574), beginning with [Configuration Manager version 1710](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1710) for the following sites:
-   A secondary site
<!--SMS.498506-->

### SQL Server 2016 Express SP1  
You can use this version of SQL Server with no minimum cumulative update version for the following sites:
-   A secondary site

### SQL Server 2016 Express
You can use this version of SQL Server with no minimum cumulative update version for the following sites:
-   A secondary site


### SQL Server 2014 Express SP2   
You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A secondary site  


### SQL Server 2014 Express SP1   
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A secondary site  

### SQL Server 2012 Express SP3  
You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A secondary site  

<!-- Support for this service pack version has been dropped by Microsoft   
### SQL Server 2012 Express SP2   
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A secondary site  
-->


##  <a name="bkmk_SQLConfig"></a> Required configurations for SQL Server  
 The following are required by all installations of SQL Server that you use for a site database (including SQL Server Express). When Configuration Manager installs SQL Server Express as part of a secondary site installation, these configurations are automatically created for you.  

 **SQL Server architecture version**  
 Configuration Manager requires a 64-bit version of SQL Server to host the site database.  

 **Database collation**  
 At each site, both the instance of SQL Server that is used for the site and the site database must use the following collation: **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager supports two exceptions to this collation to meet standards that are defined in GB18030 for use in China. For more information, see [International support in System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Database compatibility level** </br>
 Configuration Manager requires that the compatibility level for the site database be no less than the lowest supported SQL Server version for your Configuration Manager version. For instance, beginning with version 1702, you need to have a [database compatibility level](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) greater than or equal to 110. <!-- SMS.506266--> 

 **SQL Server features**  
 Only the **Database Engine Services** feature is required for each site server.  

 Configuration Manager database replication doesn't require the **SQL Server replication** feature. However, this SQL Server configuration is required when you use [database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Windows authentication**  
 Configuration Manager requires **Windows authentication** to validate connections to the database.  

 **SQL Server instance**  
 You must use a dedicated instance of SQL Server for each site. The instance can be a **named instance** or the **default instance**.  

 **SQL Server memory**  
 Reserve memory for SQL Server by using SQL Server Management Studio and setting the **Minimum server memory** setting under **Server Memory Options**. For more information about how to set this, see [How to: Set a Fixed Amount of Memory (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **For a database server that is installed on the same computer as the site server** Limit the memory for SQL Server to 50 to 80 percent of the available addressable system memory.  

-   **For a dedicated database server (remote from the site server)** Limit the memory for SQL Server to 80 to 90 percent of the available addressable system memory.  

-   **For a memory reserve for the buffer pool of each SQL Server instance in use:**  

    -   For a central administration site: Set a minimum of 8 gigabytes (GB).  
    -   For a primary site: Set a minimum of 8 gigabytes (GB).  
    -   For a secondary site: Set a minimum of 4 gigabytes (GB).  

**SQL nested triggers**  
 [SQL nested triggers](http://go.microsoft.com/fwlink/?LinkId=528802) must be enabled.  

 **SQL Server CLR integration**  
  The site database requires SQL Server common language runtime (CLR) to be enabled. This is enabled automatically when Configuration Manager installs. For more information about CLR, see [Introduction to SQL Server CLR Integration](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx).  

##  <a name="bkmk_optional"></a> Optional configurations for SQL Server  
 The following configurations are optional for each database that uses a full SQL Server installation.  

 **SQL Server service**  
 You can configure the SQL Server service to run using:  

-   A *low rights domain user* account:  

    -   This is a best practice and might require you to manually register the service principal name (SPN) for the account.  

-   The **local system** account of the computer that runs SQL Server:  

    -   Use the local system account to simplify the configuration process.  
    -   When you use the local system account, Configuration Manager automatically registers the SPN for the SQL Server service.  
    -   Be aware that using the local system account for the SQL Server service is not a SQL Server best practice.  

When the computer running SQL Server doesn't use its local system account to run the SQL Server service, you must configure the SPN of the account that runs the SQL Server service in Active Directory Domain Services. (When the system account is used, the SPN is automatically registered for you.)

For information about SPNs for the site database, see [Manage the SPN for the site database server](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) in the [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) article.  

For information about how to change the account that is used by the SQL Server service, see [How to: Change the Service Startup Account for SQL Server (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services**  
SQL Server Reporting Services is required for installing a reporting services point that lets you run reports.  

> [!IMPORTANT]  
> After you upgrade SQL Server from a previous version, you might see the following error:  *Report Builder Does Not Exist*.    
> To resolve this error, you must reinstall the reporting services point site system role.

**SQL Server ports**  
For communication to the SQL Server database engine and for intersite replication, you can use the default SQL Server port configurations or specify custom ports:  

-   **Intersite communications** use the SQL Server Service Broker, which uses port TCP 4022 by default.  
-   **Intrasite communications** between the SQL Server database engine and various Configuration Manager site system roles use port TCP 1433 by default. The following site system roles communicate directly with the SQL Server database:  

    -   Management point  
    -   SMS Provider computer  
    -   Reporting services point  
    -   Site server  

When a computer running SQL Server hosts a database from more than one site, each database must use a separate instance of SQL Server. Also, each instance must be configured to use a unique set of ports.  

> [!WARNING]  
>  Configuration Manager doesn't support dynamic ports. Because SQL Server named instances by default use dynamic ports for connections to the database engine, when you use a named instance, you must manually configure the static port that you want to use for intrasite communication.  

If you have a firewall enabled on the computer that is running SQL Server, make sure that it is configured to allow the ports that are being used by your deployment and at any locations on the network between computers that communicate with the SQL Server.  

For an example of how to configure SQL Server to use a specific port, see [How to: Configure a Server to Listen on a Specific TCP Port (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) in the SQL Server TechNet library.  

## Upgrade options for SQL Server
If you need to upgrade your version of SQL Server, we recommend the following methods, from easy to more complex.
1. [Upgrade SQL Server in-place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommended).
2. Install a new version of SQL Server on a new computer, and then [use the database move option](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) of Configuration Manager setup to point your site server to the new SQL Server.
3. Use [backup and recovery](/sccm/protect/understand/backup-and-recovery). Using backup and recovery for a SQL upgrade scenario is supported. You can ignore the SQL versioning requirement when reviewing [Considerations before recovering a site](/sccm/protect/understand/recover-sites.md#considerations-before-recovering-a-site). 
