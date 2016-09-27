---
title: "Supported operating systems for System Center Configuration Manager  site system servers"
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns

---
# Supported operating systems for System Center Configuration Manager  site system servers

This article details the Windows versions that you can use to host a System Center Configuration Manager site or site system role.


Use the information in this topic with the information in the following articles:
-   [Recommended hardware for Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site and site system prerequisitesfor Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Size and scale numbers for Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## Windows Server 2012 R2 (x64) - Standard, Datacenter  
**Site servers:**  

-   Central administration site  

-   Primary site  

-   Secondary site  

**Site system servers:**  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Asset Intelligence synchronization point  

-   Certificate registration point  

-   Distribution point  

     Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Reporting services point  

-   Service connection point  

-   Site database server  

     Site database servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](http://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base. Additionally, secondary site servers are not supported on any domain controller.  

-   SMS_Provider  

-   Software Update point  

-   State migration point  

## Windows Server 2012 (x64) - Standard, Datacenter  
**Site servers:**  

-   Central administration site  

-   Primary site  

-   Secondary site  

**Site system servers:**  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Asset Intelligence synchronization point  

-   Certificate registration point  

-   Distribution point  

     Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Reporting services point  

-   Service connection point  

-   Site database server  

     Site database servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](http://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base. Additionally, secondary site servers are not supported on any domain controller.  

-   SMS_Provider  

-   Software Update point  

-   State migration point  

## Windows Server 2008 R2 with SP1 (x64)   - Standard, Enterprise, Datacenter  
 Windows Server 2008 R2 is now in extended support and no longer in maintstream support, as detailed by the  [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information regarding future support for these operating systems as site system servers with Configuration Manager, see [Removed and deprecated features for System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**Site servers:**  

-   Central administration site  

-   Primary site  

-   Secondary site  

**Site system servers:**  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Asset Intelligence synchronization point  

-   Certificate registration point  

-   Distribution point  

     Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Reporting services point  

-   Service connection point  

-   Site database server  

     Site database servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](http://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base. Additionally, secondary site servers are not supported on any domain controller.  

-   SMS_Provider  

-   Software Update point  

-   State migration point  

## Windows Server 2008 with SP2 (x86, x64) - Standard, Enterprise, Datacenter  
 Windows Server 2008 is now in extended support and no longer in maintstream support, as detailed  by the  [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information regarding future support for these operating systems as site system servers with Configuration Manager, see [Removed and deprecated features for System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**Site servers:**  

-   Central administration site  

-   Primary site  

-   Secondary site  

**Site system servers:**  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Asset Intelligence synchronization point  

-   Certificate registration point  

-   Distribution point  

    -   Distribution points on this operating system do not support Multicast.  

    -   Distribution points on this operating system are supported for PXE, but do not support network booting of client computers in EFI mode. Client computers with BIOS or with EFI booting in legacy mode are supported.  

    -   Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Reporting services point  

-   Service connection point  

-   Site database server  

     Site database servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](http://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base. Additionally, secondary site servers are not supported on any domain controller.  

-   SMS_Provider  

-   Software Update point  

-   State migration point  

## Windows 10 (x86, x64) - Pro, Enterprise  
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this operating system are not supported for PXE.  

    -   Distribution points on this operating system version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## Windows 8.1 (x86, x64) - Professional, Enterprise  
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this operating system are not supported for PXE.  

    -   Distribution points on this operating system version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## Windows 8 (x86, x64) - Professional, Enterprise Distribution point  
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this operating system are not supported for PXE.  

    -   Distribution points on this operating system version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## Windows 7 with SP1 (x86, x64) - Professional, Enterprise, Ultimate  
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this operating system are not supported for PXE.  

    -   Distribution points on this operating system version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements and in some cases support installation not only on servers, but on client operating systems. For more information about the options available for distribution points, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## The server core installation of Windows Server 2012  
 In addition to the preceding operating systems, the  server core installation of Windows Server 2012 is supported for use as a distribution points with the following limitations:  

-   Only x64 is supported  

-   Distribution points on this operating system does not support PXE or Multicast  

## The server core installation of Windows Server 2012 R2  
 In addition to the preceding operating systems, the  server core installation of Windows Server 2012 R2 is supported for use as a distribution points with the following limitations:  

-   Only x64 is supported  

-   Distribution points on this operating system does not support PXE or Multicast  

