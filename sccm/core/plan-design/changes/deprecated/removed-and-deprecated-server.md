---
title: Deprecated for site servers
titleSuffix: Configuration Manager
description: Learn about the products and operating systems that Configuration Manager no longer supports for site servers.
ms.date: 01/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Removed and deprecated for Configuration Manager site servers

*Applies to: System Center Configuration Manager (Current Branch)*

This article describes products and operating systems that are removed from support for Configuration Manager site servers, or will be removed in a future update (deprecated). It provides early notice about future changes that might affect your use of Configuration Manager.  

This information may change in the future. It might not include each deprecated feature, product, or operating system.  



## Server OS  

|**Operating systems**|**Deprecation first announced**|**Support removed** |  
|-|-|-| 
|Windows Server 2008 R2 with SP1|July 10, 2015| Version 1702 <sup>[Note 1](#bkmk_note1)</sup>| 
|Windows Server 2008 with SP2|July 10, 2015|Version 1511 <sup>[Note 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a> Note 1: Windows Server 2008 R2 with SP1
Windows Server 2008 R2 with Service Pack 1 isn't supported for site servers or most site system roles. This OS is still supported for the distribution point role. This support includes pull-distribution points, PXE, and multicast. 

> [!Important]  
> The extended support end date for Windows Server 2008 R2 with SP1 is January 14, 2020. After this date, Configuration Manager won't support this OS in any capacity. 

You can upgrade the site server OS from Windows Server 2008 R2 to Windows Server 2012 R2. For more information, see [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2).  


#### <a name="bkmk_note2"></a> Note 2: Windows Server 2008 with SP2
Windows Server 2008 with Service Pack 2 isn't supported for site servers or most site system roles. This OS is still supported for the distribution point role. This support includes pull-distribution points, PXE, and multicast. 

> [!Important]  
> The extended support end date for Windows Server 2008 with SP2 is January 14, 2020. After this date, Configuration Manager won't support this OS in any capacity.  



## SQL Server   

|**SQL Server versions**|**Deprecation first announced**|**Support removed**|   
|-|-|-| 
|SQL Server 2008 R2|July 10, 2015|Version 1702| 
|SQL Server 2008|July 10, 2015|Version 1511|  


If you need to upgrade your version of SQL Server, we recommend the following methods, from easy to more complex:

1. [Upgrade SQL Server in-place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommended).  

2. Install a new version of SQL Server on a new computer. Then to point your site server at the new SQL Server, [use the database move option](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) of Configuration Manager setup.  

3. Use [backup and recovery](/sccm/protect/understand/backup-and-recovery).  



## More information

For more information, see the following articles: 

- [Removed and deprecated](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle)  

- [Support for current branch versions of Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)  

