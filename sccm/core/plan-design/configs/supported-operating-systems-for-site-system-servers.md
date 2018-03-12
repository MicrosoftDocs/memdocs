---
title: Supported site system servers
titleSuffix: Configuration Manager
description: Learn which Windows versions you can use to host a System Center Configuration Manager site or site system role.
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: mestew
ms.author: mstewart
manager: dougeby

---
# Supported operating systems for System Center Configuration Manager site system servers

*Applies to: System Center Configuration Manager (Current Branch)*


This article details the Windows versions that you can use to host a System Center Configuration Manager site or site system role.


Use the information in this article with the information in the following articles:
-   [Recommended hardware for Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site and site system prerequisites for Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Size and scale numbers for Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## Windows Server 2016: Standard and Datacenter
With the hotfix rollup from KB3186654 this OS is supported for the following roles:

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

     Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Management point

-   Reporting services point  

-   Service connection point  

-   Site database server  

     Site database servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](https://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base. Additionally, secondary site servers are not supported on any domain controller.  

-   SMS_Provider  

-   Software update point  

-   State migration point



## Windows Server 2012 R2 (x64): Standard and Datacenter  
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

     Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Management point

-   Reporting services point  

-   Service connection point  

-   Site database server  

     Site database servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](https://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base. Additionally, secondary site servers are not supported on any domain controller.  

-   SMS_Provider  

-   Software update point  

-   State migration point  

## Windows Server 2012 (x64): Standard and Datacenter  
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

     Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Endpoint Protection point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Management point

-   Reporting services point  

-   Service connection point  

-   Site database server  

     Site database servers are not supported on a read-only domain controller (RODC). For more information, see [You may encounter problems when installing SQL Server on a domain controller](https://go.microsoft.com/fwlink/p/?LinkId=264856) in the Microsoft Knowledge Base. Additionally, secondary site servers are not supported on any domain controller.  

-   SMS_Provider  

-   Software update point  

-   State migration point  



## Windows Server 2008 R2 with SP1 (x64): Standard, Enterprise, and Datacenter  
 Windows Server 2008 R2 is now in extended support and no longer in mainstream support, as detailed in  [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

 This OS isn't supported for site servers or most site system roles. It is still supported for the distribution point site system role, including pull-distribution points and for PXE and multicast.

**Site system servers:**  
-   Distribution point  

    -   Distribution points on this OS do not support Multicast.  

    -   Distribution points on this OS are supported for PXE.

    -   Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise, and Datacenter  
 Windows Server 2008 is now in extended support and no longer in mainstream support, as detailed in  [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

This OS isn't supported for site servers or site system roles, except for the distribution point and pull-distribution point. You can continue to use this OS as a distribution point until deprecation of this support is announced, or this OS's extended support period expires. For more information, see [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095).

**Site system servers:**  
-   Distribution point  

    -   Distribution points on this OS do not support Multicast.  

    -   Distribution points on this OS are supported for PXE, but do not support network booting of client computers in EFI mode. Client computers with BIOS or with EFI booting in legacy mode are supported.  

    -   Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## Windows 10 (x86, x64): Pro and Enterprise  
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this OS are not supported for PXE with the default Windows Deployment Services. Starting in version 1802, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe). 

    -   Distribution points on this OS version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## Windows 8.1 (x86, x64): Professional and Enterprise  
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this OS are not supported for PXE with the default Windows Deployment Services. Starting in version 1802, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

    -   Distribution points on this OS version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## Windows 7 with SP1 (x86, x64): Professional, Enterprise, and Ultimate  
**Site system servers:**  

-   Distribution point  

    -   Distribution points on this OS are not supported for PXE with the default Windows Deployment Services. Starting in version 1802, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

    -   Distribution points on this OS version do not support Multicast.  

    -   Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information about the options that are available for distribution points, see [Manage content and content infrastructure](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## The server core installation of Windows Server 2016
With the hotfix rollup from KB3186654, this OS is supported for use as a distribution point with the following limitations:  
  -   Only the x64-bit version is supported.
  -   Distribution points on this OS do not support PXE or Multicast with the default Windows Deployment Services. Starting in version 1802, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  



## The server core installation of Windows Server 2012 R2  
 The server core installation of Windows Server 2012 R2 is supported for use as a distribution point with the following limitations:  

-   Only the x64-bit version is supported.

-   Distribution points on this OS do not support PXE or Multicast with the default Windows Deployment Services. Starting in version 1802, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  



## The server core installation of Windows Server 2012  
 The server core installation of Windows Server 2012 is supported for use as a distribution point with the following limitations:  

-   Only the 64-bit version is supported.  

-   Distribution points on this OS do not support PXE or Multicast with the default Windows Deployment Services. Starting in version 1802, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).
