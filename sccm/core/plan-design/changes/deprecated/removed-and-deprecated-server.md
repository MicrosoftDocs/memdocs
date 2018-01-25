---
title: "Deprecated for Configuration Manager site servers"
titleSuffix: "Configuration Manager"
description: "Learn about the products and operating systems that System Center Configuration Manager no longer supports for site servers."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
caps.latest.revision: 15
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: angrobe
---

# Removed and deprecated for System Center Configuration Manager site servers

*Applies to: System Center Configuration Manager (Current Branch)*

This article describes products and operating systems that are removed from support for System Center Configuration Manager site servers, or will be removed in a future update (deprecated). This article provides early notice about future changes that might affect your use of Configuration Manager.  

This information is subject to change with future releases, and might not include each deprecated feature, product, or operating system.  


## Deprecated server operating systems  

|**Operating systems**|**Deprecation first announced**|**Support removed** |  
|-|-|-| 
|Windows Server 2008 R2|July 10, 2015| Version 1702  (See note 1)| 
|Windows Server 2008|July 10, 2015|Version 1511 </br></br>Support as a site system is removed. (See note 2).|  

>[!NOTE]
>-   Note 1: Beginning with version 1702, this operating system is not supported for site servers or most site system roles. However, versions prior to 1702 continue to support its use. This operating system remains supported for the distribution point site system role (including pull-distribution points, and for PXE and multicast) until deprecation of support is announced, or the operating system's extended support period expires. Beginning with version 1602, you can in-place upgrade the operating system of a site server from Windows Server 2008 R2 to Windows Server 2012 R2.  
>- For more information about in-place upgrade of a site servers operating system, see the [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2) section in [Upgrade on-premises infrastructure that supports System Center Configuration Manager](/sccm/core/servers/manage/upgrade-on-premises-infrastructure).

>[!NOTE]
>-   Note 2: This operating system is not supported for site servers or site system roles except for distribution point and pull-distribution point. You can continue to use this operating system as a distribution point until deprecation of support is announced, or the operating system's extended support period expires. For more information, see [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095).

## Deprecated support for SQL Server versions as a site database  

|**SQL Server versions**|**Deprecation first announced**|**Support removed**|   
|-|-|-| 
|SQL Server 2008 R2|July 10, 2015|Version 1702| 
|SQL Server 2008|July 10, 2015|Version 1511|  


If you need to upgrade your version of SQL Server, we recommend the following methods, from easy to more complex.
1. [Upgrade SQL Server in-place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommended).
2. Install a new version of SQL Server on a new computer. Then [use the database move option](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) of Configuration Manager setup to point your site server at the new SQL Server.
3. Use [backup and recovery](/sccm/protect/understand/backup-and-recovery).


## More information
For more information, see:
 - [Removed and deprecated](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - The [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) website.
 - [Support for current branch versions of Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).