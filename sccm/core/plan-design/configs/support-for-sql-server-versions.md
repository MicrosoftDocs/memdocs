---
title: "Support for SQL Server | System Center Configuration Manager"
description: "Get SQL Server version and configuration requirements for hosting a System Center Configuration Manager site database."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brendunsms.author: brendunsmanager: angrobe

---
# Support for SQL Server versions for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Each System Center Configuration Manager site requires a supported SQL Server version and configuration to host the site database.  

##  <a name="bkmk_Instances"></a> SQL Server instances and locations  
 **Central administration site and  Primary sites:**  

The site database must use a full install of SQL Server.  

 The location of SQL Server can be on:  

-   The site server computer  
-   A computer that is remote from the site server  

The following instances are supported:  

-   Default or named instance of SQL Server  
-   Multiple instance configurations  
-   SQL Server cluster  - See [Use a SQL Server cluster to host the site database](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)
-   SQL Server AlwaysOn availability group - This option requires Configuration Manager version 1602 or later. For details see [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)  

> [!NOTE]  
>  A SQL Server cluster in a Network Load Balancing (NLB) cluster configuration is not supported. Additionally, SQL Server database mirroring technology and peer-to-peer replication are not supported. SQL Server standard transactional replication is supported only for replicating objects to management points that are configured to use [database replicas](https://technet.microsoft.com/library/mt608546.aspx).  


 **Secondary Sites:**  

 The site database can use the default instance of a full install of SQL Server, or SQL Server Express  

 The location of SQL Server must be on the site server computer  

##  <a name="bkmk_SQLVersions"></a> Supported versions of SQL Server  
 In a hierarchy with multiple sites, different sites can use different versions of SQL Server to host the site database so long as the versions of SQL Server you use are supported by Configuration Manager.  

 The following versions of SQL Server are supported with System Center Configuration Manager version 1511 and later.  

> [!IMPORTANT]  
>  Use of SQL Server Standard for the database at the central administration site limits the total number of clients a hierarchy can support. See [Size and scale numbers](../../../core/plan-design/configs/size-and-scale-numbers.md).

### SQL Server 2016 - Standard, Enterprise  

Supported for use with version 1606.   
You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Central administration site  
-   Primary site  
-   Secondary site  


### SQL Server 2014 SP2 - Standard, Enterprise  

Supported for version 1511 and later.  
You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Central administration site  
-   Primary site  
-   Secondary site  



### SQL Server 2014 SP1 - Standard, Enterprise  

Supported for version 1511 and later.  
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Central administration site  
-   Primary site  
-   Secondary site  


### SQL Server 2012 SP3 - Standard, Enterprise  

Supported for version 1511 and later.  
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Central administration site  
-   Primary site  
-   Secondary site  


### SQL Server 2012 SP2 - Standard, Enterprise  

Supported for version 1511 and later.  
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Central administration site  
-   Primary site  
-   Secondary site  


### SQL Server 2008 R2 SP3 - Standard, Enterprise, Datacenter  

Supported for version 1511 and later.    
You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Central administration site  
-   Primary site  
-   Secondary site  

### SQL Server 2016 Express
Supported for use with version 1606.  
You can use this version of SQL Server with no minimum cumulative update version for the following:
-   Secondary site

### SQL Server 2014 Express SP2  
Supported for use with version 1511 and later.  
You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Secondary site  


### SQL Server 2014 Express SP1  
 Supported for use with version 1511 and later.   
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Secondary site  

### SQL Server 2012 Express SP3  
Supported for use with version 1511 and later.   
You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Secondary site  

### SQL Server 2012 Express SP2  
 Supported for use with version 1511 and later.  
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   Secondary site  

##  <a name="bkmk_SQLConfig"></a> Required configurations for SQL Server  
 The following are required by all installations of SQL Server you use for a site database, (including SQL Server Express). When Configuration Manager installs SQL Server Express as part of as secondary site install, these configurations are automatically made for you.  

 **SQL Server architecture version:**  
 Configuration Manager requires a 64-bit version of SQL Server to host the site database.  

 **Database collation:**  
 At each site, both the instance of SQL Server that is used for the site and the site database must use the following collation: **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager supports two exceptions to this collation to meet standards that are defined in GB18030 for use in China. For more information, see [International support in System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **SQL Server features:**  
 Only the **Database Engine Services** feature is required for each site server.  

 Configuration Manager database replication does not require the **SQL Server replication** feature. However, this SQL Server configuration is required if you will  use [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Windows Authentication:**  
 Configuration Manager requires **Windows authentication** to validate connections to the database.  

 **SQL Server instance:**  
 You must use a dedicated instance of SQL Server for each site. This can be a **named instance** or the **default instance**.  

 **SQL Server memory:**  
 Reserve  memory for SQL Server by using SQL Server Management Studio and setting the **Minimum server memory** setting under **Server Memory Options**. For more information about how to set a fixed amount of memory, see [How to: Set a Fixed Amount of Memory (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Database server that is installed on the same computer as the site server:** - Limit the memory for SQL Server to 50 to 80 percent of the available addressable system memory.  

-   **Dedicated database server (remote from the site server):** -   Limit the memory for SQL Server to 80 to 90 percent of the available addressable system memory.  

-   **Memory reserve for the buffer pool of each SQL Server instance in use:**  

    -   Central administration site: minimum of 8 gigabytes (GB)  
    -   Primary site: minimum of 8 gigabytes (GB)  
    -   Secondary site: minimum of 4 gigabytes (GB)  

 **SQL nested triggers:**  

 [SQL nested triggers](http://go.microsoft.com/fwlink/?LinkId=528802) must be enabled.  

 **SQL Server CLR integration**  

  The site database requires SQL Server common language runtime (CLR) to be enabled. This is enabled automatically when Configuration Manager installs. For more information about CLR, see [Introduction to SQL Server CLR Integration](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)  

##  <a name="bkmk_optional"></a> Optional configurations for SQL Server  
 The following configurations are optional for each database that uses a full SQL Server installation.  

 **SQL Server service:**  
 You can configure the SQL Server service to run using:  

-   **Domain local user** account:  

    -   This is a best practice and might require you to manually register the Service Principle Name (SPN) for the account.  

-   **Local system** account  of the computer that runs SQL Server:  

    -   Use the local system account to simplify the configuration process.  
    -   When you use the local system account, Configuration Manager automatically registers the SPN for the SQL Server service.  
    -   Be aware that using the local system account for the SQL Server service is not a SQL Server best practice.  

When the SQL Server does not use that computers local system account to run SQL Server services, you must configure the Service Principal Name (SPN) of the account that runs SQL Server services in Active directory Domain services. (When the system account is used, the SPN is automatically registered for you).

For information about SPNs for the site database, see  [Manage the SPN for the site database server](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) in the [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) topic.  

For information about how to change the account that is used by the SQL Service, see [How to: Change the Service Startup Account for SQL Server (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services:**  
Required to install a reporting services point that lets you run reports.  

**SQL Server ports:**  
For communication to the SQL Server database engine, and for intersite replication, you can use the default SQL Server port configurations or specify custom ports:  

-   **Intersite communications** use the SQL Server Service Broker, which by default uses port TCP 4022.  
-   **Intrasite communication** between the SQL Server database engine and various Configuration Manager site system roles by default use port TCP 1433. The following site system roles communicate directly with the SQL Server database:  

    -   Management point  
    -   SMS Provider computer  
    -   Reporting Services point  
    -   Site server  

When a SQL Server hosts a database from more than one site, each database must use a separate instance of SQL Server, and each instance must be configured to use a unique set of ports.  

> [!WARNING]  
>  Configuration Manager does not support dynamic ports. Because SQL Server named instances by default use dynamic ports for connections to the database engine, when you use a named instance, you must manually configure the static port that you want to use for intrasite communication.  

If you have a firewall enabled on the computer that is running SQL Server, make sure that it is configured to allow the ports that are being used by your deployment and at any locations on the network between computers that communicate with the SQL Server.  

For an example of how to configure SQL Server to use a specific port, see [How to: Configure a Server to Listen on a Specific TCP Port (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) in the SQL Server TechNet library.  
