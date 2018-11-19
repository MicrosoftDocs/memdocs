---
title: Supported site system servers
titleSuffix: Configuration Manager
description: Learn which Windows versions you can use to host a Configuration Manager site or site system role.
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Supported operating systems for Configuration Manager site system servers

*Applies to: System Center Configuration Manager (Current Branch)*


This article details the Windows versions that you can use to host a Configuration Manager site or site system role.


Use the information in this article with the information in the following articles:
-   [Recommended hardware for Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)
-   [Site and site system prerequisites for Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
-   [Size and scale numbers for Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers)



## <a name="bkmk_2019"></a> Windows Server 2019

*Applies to Windows Server 2019: Standard and Datacenter* 

Starting in version 1810, this OS version is supported for the following roles:

#### Site servers

-   Central administration site  
-   Primary site  
-   Secondary site  

#### Site system servers

-   Application Catalog web service point  
-   Application Catalog website point  
-   Asset Intelligence synchronization point  
-   Certificate registration point  
-   Cloud management gateway connection point  
-   Data warehouse service point  
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
-   Endpoint Protection point  
-   Enrollment point  
-   Enrollment proxy point  
-   Fallback status point  
-   Management point
-   Reporting services point  
-   Service connection point  
-   Site database server <sup>[Note 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Software update point  
-   State migration point



## <a name="bkmk_2016"></a> Windows Server 2016

*Applies to Windows Server 2016: Standard and Datacenter*

This OS version is supported for the following roles:

#### Site servers

-   Central administration site  
-   Primary site  
-   Secondary site  

#### Site system servers

-   Application Catalog web service point  
-   Application Catalog website point  
-   Asset Intelligence synchronization point  
-   Certificate registration point  
-   Cloud management gateway connection point  
-   Data warehouse service point  
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
-   Endpoint Protection point  
-   Enrollment point  
-   Enrollment proxy point  
-   Fallback status point  
-   Management point
-   Reporting services point  
-   Service connection point  
-   Site database server <sup>[Note 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Software update point  
-   State migration point



## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### Site system server

-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  



## <a name="bkmk_2012r2"></a> Windows Server 2012 R2 

*Applies to Windows Server 2012 R2: Standard and Datacenter*

#### Site servers

-   Central administration site  
-   Primary site  
-   Secondary site  

#### Site system servers

-   Application Catalog web service point  
-   Application Catalog website point  
-   Asset Intelligence synchronization point  
-   Certificate registration point  
-   Cloud management gateway connection point  
-   Data warehouse service point  
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
-   Endpoint Protection point  
-   Enrollment point  
-   Enrollment proxy point  
-   Fallback status point  
-   Management point
-   Reporting services point  
-   Service connection point  
-   Site database server <sup>[Note 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Software update point  
-   State migration point  



## <a name="bkmk_2012"></a> Windows Server 2012  

*Applies to Windows Server 2012: Standard and Datacenter*

#### Site servers

-   Central administration site  
-   Primary site  
-   Secondary site  

#### Site system servers

-   Application Catalog web service point  
-   Application Catalog website point  
-   Asset Intelligence synchronization point  
-   Certificate registration point  
-   Cloud management gateway connection point  
-   Data warehouse service point  
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
-   Endpoint Protection point  
-   Enrollment point  
-   Enrollment proxy point  
-   Fallback status point  
-   Management point
-   Reporting services point  
-   Service connection point  
-   Site database server <sup>[Note 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   Software update point  
-   State migration point  



## <a name="bkmk_2008r2sp1"></a> Windows Server 2008 R2 with SP1   

*Applies to Windows Server 2008 R2 with Service Pack 1: Standard, Enterprise, and Datacenter*

Windows Server 2008 R2 is now in extended support and no longer in mainstream support, as detailed in [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

This OS isn't supported for site servers or most site system roles. It's still supported for the distribution point site system role, including pull-distribution points and for PXE and multicast.

#### Site system servers
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

    - Distribution points on this OS support PXE and multicast.  



## <a name="bkmk_2008sp2"></a> Windows Server 2008 with SP2  

*Applies to Windows Server 2008 with Service Pack 2 (x86, x64): Standard, Enterprise, and Datacenter*

Windows Server 2008 with Service Pack 2 (SP2) is now in extended support and no longer in mainstream support, as detailed in [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

This OS isn't supported for site servers or site system roles, except for the distribution point and pull-distribution point. Continue to use this OS as a distribution point until deprecation of this support is announced, or this OS's extended support period expires. For more information, see [Installation of Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095).

#### Site system servers
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

    -   Distribution points on this OS support PXE and multicast.  

    -   Distribution points on this OS don't support network booting of client computers in EFI mode. Client computers with BIOS or with EFI booting in legacy mode are supported.  



## <a name="bkmk_client"></a> Client OS versions

The following client OS versions are supported for use as a **distribution point** <sup>[Note 1](#bkmk_note1)</sup>:  

- Windows 10 (x86, x64): Pro and Enterprise
- Windows 8.1 (x86, x64): Professional and Enterprise
- Windows 7 with SP1 (x86, x64): Professional, Enterprise, and Ultimate

This support has the following limitation:  

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core"></a> Server core installations

The server core installation of the following server OS versions are supported for use as a **distribution point**: 

- Windows Server, version 1809 (starting in Configuration Manager, version 1810)  
- Windows Server, version 1803 (starting in Configuration Manager, version 1802)  
- Windows Server, version 1709 (starting in Configuration Manager, version 1710)  
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

This support has the following limitation:  

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## General notes

#### <a name="bkmk_note1"></a> Note 1: Distribution points
Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information, see [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

#### <a name="bkmk_note2"></a> Note 2: Site database servers
Site database servers aren't supported on a read-only domain controller (RODC). For more information, see the Microsoft Support article: [You may encounter problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911). 

Additionally, secondary site servers aren't supported on any domain controller.  
