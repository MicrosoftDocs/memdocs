---
title: Upgrade on-premises infrastructure
titleSuffix: Configuration Manager
description: Learn how to upgrade infrastructure, such as SQL Server and the OS of site systems.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Upgrade on-premises infrastructure that supports System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the information in this article to help you upgrade the server infrastructure that runs Configuration Manager.  

 - If you want to *upgrade* from an earlier version of Configuration Manager to System Center Configuration Manager, current branch, see [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- If you want to *update* your System Center Configuration Manager, current branch, infrastructure to a new version, see [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates).



##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Upgrade the OS of site systems  
 Configuration Manager supports the in-place upgrade of the operating system (OS) of servers that host a site server and of remote servers that host any site system role, in the following situations:  

-   In-place upgrade to a later Windows Server service pack if the resulting service pack level of Windows remains supported by Configuration Manager.  
-   In-place upgrade from:
    - Windows Server 2012 R2 to Windows Server 2016 ([See additional details](#bkmk_2016)).
    - Windows Server 2012 to Windows Server 2016 ([See additional details](#bkmk_2016)).
    - Windows Server 2012 to Windows Server 2012 R2 ([See additional details](#bkmk_2012r2)).
    - Windows Server 2008 R2 to Windows Server 2012 R2 ([See additional details](#bkmk_from2008r2).

    > [!WARNING]  
    >  Before you upgrade to a different OS, *you must uninstall WSUS* from the server. You may keep the SUSDB and reattach it once WSUS is reinstalled. 
    >  For more information about this critical step, see the "New and changed functionality" section in [Windows Server Update Services Overview](https://technet.microsoft.com/library/hh852345.aspx) in the Windows Server documentation.  

To upgrade a server, use the upgrade procedures provided by the OS you're upgrading to. See the following articles:
  -  [Upgrade Options for Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) in the Windows Server documentation.  
  - [Upgrade and conversion options for Windows Server 2016](/windows-server/get-started/supported-upgrade-paths) in the Windows Server documentation.

### <a name="bkmk_2016"></a>  Upgrade Windows Server 2012 or Windows Server 2012 R2 to 2016
When you upgrade either Windows Server 2012 or Windows Server 2012 R2 to Windows Server 2016, the following apply:


#### Before upgrade  
- 	Remove the System Center Endpoint Protection (SCEP) client. Windows Server 2016 has Windows Defender built in, which replaces the SCEP client. The presence of the SCEP client can prevent an upgrade to Windows Server 2016.
-   Remove the WSUS role from the server if it is installed. You may keep the SUSDB and reattach it once WSUS is reinstalled.

#### After upgrade   
- 	Ensure Windows Defender is enabled, set for automatic start, and running.
- 	Ensure the following Configuration Manager services are running:
  - 	SMS_EXECUTIVE
  - 	SMS_SITE_COMPONENT_MANAGER


- 	Ensure the **Windows Process Activation** and **WWW/W3svc** services are enabled, set for automatic start, and running for the following site system roles (these services are disabled during upgrade):
  - 	Site server
  - 	Management point
  - 	Application Catalog web service point
  - 	Application Catalog website point

- 	Ensure each server that hosts a site system role continues to meet all of the [prerequisites for site system roles](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) that run on that server. For example, you might need to reinstall BITS, WSUS, or configure specific settings for IIS.

-   After restoring any missing prerequisites, restart the server one more time to ensure services are started and operational.

-   If you are upgrading the primary site server, then [run a site reset](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).

#### Known issue for remote Configuration Manager consoles   
After you upgrade the site server or a server that hosts an instance of the SMS_Provider to Windows Server 2016, administrative users might not be able to connect a Configuration Manager console to the site. To work around this problem, you must manually restore permissions for the SMS Admins group in WMI. Permissions must be set on the site server, and on each remote server that hosts an instance of the SMS_Provider:

1. On the applicable servers, open the Microsoft Management Console (MMC) and add the snap-in for  **WMI Control**, and then select **Local computer**.
2. In the MMC, open the **Properties** of **WMI Control (Local)** and select the **Security** tab.
3. Expand the tree below Root, select the **SMS** node, and then choose **Security**.  Ensure the **SMS Admins** group has the following permissions:
  - 	Enable Account
  - 	Remote Enable
4. On the **Security tab** below the **SMS** node, select the **site_&lt;sitecode**> node, and then choose **Security**. Ensure the **SMS Admins** group has the following permissions:
  -   Execute Methods
  -   Provider Write
  -   Enable Account
  -   Remote Enable
5. Save the permissions to restore access for the Configuration Manager console.


### <a name="bkmk_2012r2"></a> Windows Server 2012 to Windows Server 2012 R2

#### Before upgrade  
-   Remove the WSUS role from the server if it is installed. You may keep the SUSDB and reattach it once WSUS is reinstalled.

#### After upgrade  
  -	Ensure the Windows Deployment Service is started and running for the following site system roles (this service is stopped during upgrade):
    - Site server
    - Management point
    - Application Catalog web service point
    - Application Catalog website point

  - 	Ensure the **Windows Process Activation** and **WWW/W3svc** services are enabled, set for automatic start, and running for the following site system roles (these services are disabled during upgrade):
    - 	Site server
    - 	Management point
    - 	Application Catalog web service point
    - 	Application Catalog website point


  - 	Ensure each server that hosts a site system role continues to meet all of the [prerequisites for site system roles](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) that run on that server. For example, you might need to reinstall BITS, WSUS, or configure specific settings for IIS.

  After restoring any missing prerequisites, restart the server one more time to ensure services are started and operational.

### <a name="bkmk_from2008r2"></a>  Upgrade Windows Server 2008 R2 to Windows Server 2012 R2
This OS upgrade scenario has the following conditions:  

#### Before upgrade  
- 	Uninstall WSUS 3.2.  
    Before you upgrade a server OS to Windows Server 2012 R2, you must uninstall WSUS 3.2 from the server. For information about this critical step, see the New and changed functionality section in [Windows Server Update Services Overview](https://technet.microsoft.com/library/hh852345.aspx) in the Windows Server documentation.

#### After upgrade  
  -	Ensure the Windows Deployment Service is started and running for the following site system roles (this service is stopped during upgrade):
    - Site server
    - Management point
    - Application Catalog web service point
    - Application Catalog website point


  - 	Ensure the **Windows Process Activation** and **WWW/W3svc** services are enabled, set for automatic start, and running for the following site system roles (these services are disabled during upgrade):
    - 	Site server
    - 	Management point
    - 	Application Catalog web service point
    - 	Application Catalog website point


  - 	Ensure each server that hosts a site system role continues to meet all of [perquisites for site system roles](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) that run on that server. For example, you might need to reinstall BITS, WSUS, or configure specific settings for IIS.

  After restoring any missing prerequisites, restart the server one more time to ensure services are started and operational.


### Unsupported upgrade scenarios
The following Windows Server upgrade scenarios are commonly asked about, but not supported by Configuration Manager:  

-   Windows Server 2008 to Windows Server 2012 or later  
-   Windows Server 2008 R2 to Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Upgrade the OS of Configuration Manager clients  
 Configuration Manager supports an in-place upgrade of the OS for Configuration Manager clients in the following situations:  

-   In-place upgrade to a later Windows service pack if the resulting service pack level remains supported by Configuration Manager.  

-   In-place upgrade of Windows from a supported version to Windows 10. For more information, see [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Build-to-build servicing upgrades of Windows 10. For more information, see [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md).  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Upgrade SQL Server on the site database server  
  Configuration Manager supports an in-place upgrade of SQL Server from a supported version of SQL on the site database server. The SQL Server upgrade scenarios in this section are supported by Configuration Manager and include requirements for each scenario.

 For information about the versions of SQL Server that are supported by Configuration Manager, see [Support for SQL Server versions](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 ### Upgrade the service pack version of SQL Server    
 Configuration Manager supports the in-place upgrade of SQL Server to a later service pack if the resulting SQL Server service pack level remains supported by Configuration Manager.

 When you have multiple Configuration Manager sites in a hierarchy, each site can run a different service pack version of SQL Server. There's no limitation to the order in which sites upgrade the service pack version of SQL Server that's used for the site database.

### Upgrade to a new version of SQL Server   
 Configuration Manager supports the in-place upgrade of SQL Server to the following versions:

 - SQL Server 2017
 - SQL Server 2016  
 - SQL Server 2014  

When you upgrade the version of SQL Server that hosts the site database, you must upgrade the SQL Server version that is used at sites in the following order:

 1. Upgrade SQL Server at the central administration site first.
 2. Upgrade secondary sites before you upgrade a secondary site's parent primary site.
 3. Upgrade parent primary sites last. These sites include both child primary sites that report to a central administration site, and stand-alone primary sites that are the top-level site of a hierarchy.

### SQL Server Cardinality Estimation level and the site database   
When a site database is upgraded from an earlier version of SQL Server, the database retains its existing SQL Cardinality Estimation (CE) level if it is at the minimum allowed for that instance of SQL Server. Upgrading SQL Server with a database at a compatibility level lower than the allowed level automatically sets the database to the lowest compatibility level allowed by SQL Server.

The following table identifies the recommended compatibility levels for Configuration Manager site databases:

|SQL Server version | Supported compatibility levels |Recommended level|
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

To identify the SQL Server CE compatibility level in use for your site database, run the following SQL query on the site database server:  
`SELECT name, compatibility_level FROM sys.databases`

 For more information on SQL CE compatibility levels and how to set them, see [ALTER DATABASE Compatibility Level (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).


For more information about upgrading SQL Server, see the following SQL Server documentation:
-   [Upgrade to SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)
-   [Upgrade to SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)
-   [Upgrade to SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  



### To upgrade SQL Server on the site database server  

1.  Stop all Configuration Manager services at the site.  
2.  Upgrade SQL Server to a supported version.  
3.  Restart the Configuration Manager services.  

> [!NOTE]  
>  When you change the SQL Server edition in use at the central administration site from a Standard edition to either a Datacenter or Enterprise edition, the database partition that limits the number of clients the hierarchy supports does not change.
