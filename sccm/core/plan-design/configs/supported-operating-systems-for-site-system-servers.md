---
title: Supported site system servers
titleSuffix: Configuration Manager
description: Learn which Windows versions you can use to host a Configuration Manager site or site system role.
ms.date: 10/02/2018
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



## <a name="bkmk_2019"></a> Windows Server 2019: Standard and Datacenter
<!--SCCMDocs-pr issue 2907-->
Starting in version 1806, Windows Server 2019 is supported for the following roles:

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



## <a name="bkmk_2016"></a> Windows Server 2016: Standard and Datacenter

With Update Rollup 1 for Configuration Manager version 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), this OS version is supported for the following roles:

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



## <a name="bkmk_2012r2"></a> Windows Server 2012 R2 (x64): Standard and Datacenter  

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



## <a name="bkmk_2012"></a> Windows Server 2012 (x64): Standard and Datacenter  

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



## <a name="bkmk_2008r2sp1"></a> Windows Server 2008 R2 with SP1 (x64): Standard, Enterprise, and Datacenter  

Windows Server 2008 R2 is now in extended support and no longer in mainstream support, as detailed in [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

This OS isn't supported for site servers or most site system roles. It's still supported for the distribution point site system role, including pull-distribution points and for PXE and multicast.

#### Site system servers
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

    - Distribution points on this OS support PXE and multicast.  



## <a name="bkmk_2008sp2"></a> Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise, and Datacenter  

Windows Server 2008 is now in extended support and no longer in mainstream support, as detailed in [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Deprecated server operating systems](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

This OS isn't supported for site servers or site system roles, except for the distribution point and pull-distribution point. Continue to use this OS as a distribution point until deprecation of this support is announced, or this OS's extended support period expires. For more information, see [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095).

#### Site system servers
-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

    -   Distribution points on this OS support PXE and multicast.  

    -   Distribution points on this OS don't support network booting of client computers in EFI mode. Client computers with BIOS or with EFI booting in legacy mode are supported.  



## <a name="bkmk_win10"></a> Windows 10 (x86, x64): Pro and Enterprise  

#### Site system servers

-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

    -   Distribution points on this OS aren't supported for PXE with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Distribution points on this OS version don't support multicast.  



## <a name="bkmk_win81"></a> Windows 8.1 (x86, x64): Professional and Enterprise  

#### Site system servers

-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

    -   Distribution points on this OS aren't supported for PXE with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Distribution points on this OS version don't support multicast.  



## <a name="bkmk_win7sp1"></a> Windows 7 with SP1 (x86, x64): Professional, Enterprise, and Ultimate  

#### Site system servers

-   Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

    -   Distribution points on this OS aren't supported for PXE with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   Distribution points on this OS version don't support multicast.  



## <a name="bkmk_core1809"></a> The server core installation of Windows Server, version 1809
<!--SCCMDocs-pr issue 2907-->
Starting in Configuration Manager 1806, [Windows Server, version 1809](https://docs.microsoft.com/windows-server/get-started/get-started-with-1809) is supported for use as a distribution point with the following limitations:  

  -   Only the x64-bit version is supported.  

  -   Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core1803"></a> The server core installation of Windows Server, version 1803
<!--503702-->
Starting in Configuration Manager 1802, [Windows Server, version 1803](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803) is supported for use as a distribution point with the following limitations:  

  -   Only the x64-bit version is supported.  

  -   Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core1709"></a> The server core installation of Windows Server, version 1709

Starting in Configuration Manager 1710, [Windows Server, version 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) is supported for use as a distribution point with the following limitations:  

  -   Only the x64-bit version is supported.  

  -   Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2016"></a> The server core installation of Windows Server 2016

With Update Rollup 1 for Configuration Manager version 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), this OS version is supported for use as a distribution point with the following limitations:  

  -   Only the x64-bit version is supported.  

  -   Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2012r2"></a> The server core installation of Windows Server 2012 R2  

The server core installation of Windows Server 2012 R2 is supported for use as a distribution point with the following limitations:  

-   Only the x64-bit version is supported.

-   Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)
.  



## <a name="bkmk_core2012"></a> The server core installation of Windows Server 2012  

The server core installation of Windows Server 2012 is supported for use as a distribution point with the following limitations:  

-   Only the 64-bit version is supported.  

-   Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).



## General notes

#### <a name="bkmk_note1"></a> Note 1: Distribution points
Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information, see [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

#### <a name="bkmk_note2"></a> Note 2: Site database servers
Site database servers aren't supported on a read-only domain controller (RODC). For more information, see the Microsoft Support article: [You may encounter problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911). 

Additionally, secondary site servers aren't supported on any domain controller.  
