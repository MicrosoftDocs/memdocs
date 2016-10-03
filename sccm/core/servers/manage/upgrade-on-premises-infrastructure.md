---
title: "Upgrade on-premises infrastructure | System Center Configuration Manager"
description: "Learn how to upgrade infrastructure, such as SQL Server and the site operating system of site systems."
ms.custom: na
ms.date: 03/11/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Upgrade on-premises infrastructure that supports System Center Configuration Manager
Use the following information to help you upgrade infrastructure that runs System Center Configuration Manager.  

##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Upgrade site operating system of site systems  
 Configuration Manager supports an in-place upgrade of the operating system of the site server  in the following situations:  

-   In-place upgrade to a higher Windows Server service pack as long as the resulting service pack level remains supported by Configuration Manager.  

-   In-place upgrade from Windows Server 2012 to Windows Server 2012 R2.  

-   Configuration Manager sites that run version 1602 or later  support the in-place upgrade of the site servers operating system from  Windows Server 2008 R2 to Windows Server 2012 R2.  

    > [!WARNING]  
    >  Before you upgrade to Windows Server 2012 R2, **you must uninstall WSUS 3.2** from the server.  
    >   
    >  For information about this critical step, see the New and changed functionality section  in [Windows Server Update Services Overview](https://technet.microsoft.com/library/hh852345.aspx) in the Windows Server documentation.  

     To upgrade a server, you use the Windows Server 2012 R2 upgrade procedures and do not need to run a Configuration Manager site server restore after the upgrade.  For upgrade procedures, see [Upgrade Options for Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) in the Windows Server documentation.  

Configuration Manager does not support the following Windows Server upgrade scenarios.  

-   Windows Server 2008 to Windows Server 2012 or later.  

-   Windows Server 2008 R2 to Windows Server 2012.  

##  <a name="BKMK_SupConfigUpgradeClient"></a> Upgrade the operating system of clients  
 Configuration Manager supports an in-place upgrade of the operating system for Configuration Manager clients in the following situations:  

-   In-place upgrade to a higher Windows service pack as long as the resulting service pack level remains supported by Configuration Manager.  

-   In-place upgrade of Windows from a supported version to Windows 10. See [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) for more information.  

-   Build-to-build servicing upgrades of Windows 10.  See [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md) for more information.  

##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Upgrade SQL Server on the site database server  
 Configuration Manager supports an in-place upgrade of SQL Server from a supported version of SQL on the site database server. The following table provides details about the upgrade scenarios supported by Configuration Manager and any requirements for each scenario.  

 For information about which versions of SQL Server are supported by Configuration Manager, see [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **When upgrading the service pack version of SQL Server:**    
 Configuration Manager supports the in-place upgrade of SQL Server to a higher service pack as long as the resulting SQL Server service pack level remains supported by Configuration Manager.

 When you have multiple Configuration Manager sites in a hierarchy, each site can run a different service pack version of SQL Server, and there is no limitation to the order in which sites upgrade the service pack version of SQL Server that is used for the site database.

 **When upgrading to a new version of SQL Server:**   
 Configuration Manager supports the in-place upgrade of SQL Server to the following versions:

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

When you upgrade the version of SQL Server that hosts the site database, you must upgrade the SQL Server version that is used at sites in the following order:

 1. Upgrade SQL Server at the central administration site first.
 2. Upgrade secondary sites before you upgrade a secondary sites parent primary site.
 3. Upgrade parent primary sites last. This includes both child primary sites that report to a central administration site, and stand-alone primary sites that are the top-level site of a hierarchy.



**For more information about SQL Server, see the SQL Server documentation on TechNet:**  
-   [Upgrade to SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120\).aspx)  

-   [Upgrade to SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110\).aspx)

-   [Upgrade to SQL Server 2016](https://technet.microsoft.com/en-us/library/bb677622(v=sql.130).aspx)



### To upgrade SQL Server on the site database server  

1.  Stop all Configuration Manager services at the site.  
2.  Upgrade SQL Server to a supported version.  
3.  Restart the Configuration Manager services.  

> [!NOTE]  
>  When you change the SQL Server edition in use at the central administration site from a Standard edition to either a Datacenter or Enterprise edition, the database partition that limits the number of clients the hierarchy supports does not change.
