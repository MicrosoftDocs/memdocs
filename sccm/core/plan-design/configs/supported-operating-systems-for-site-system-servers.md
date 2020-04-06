---
title: Supported site system servers
titleSuffix: Configuration Manager
description: Learn which Windows versions you can use to host a Configuration Manager site or site system role.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: mestew
ms.author: mstewart
manager: dougeby
---

# Supported operating systems for Configuration Manager site system servers

*Applies to: Configuration Manager (current branch)*

This article details the Windows versions that you can use to host a Configuration Manager site or site system role.

Use the information in this article with the information in the following articles:

- [Recommended hardware for Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)
- [Site and site system prerequisites for Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Size and scale numbers for Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers)

## <a name="bkmk_2019"></a> Windows Server 2019

*Applies to Windows Server 2019: Standard and Datacenter* 

Starting in version 1810, this OS version is supported for the following roles:

#### Site servers

- Central administration site  
- Primary site  
- Secondary site  

#### Site system servers

- Application Catalog web service point  
- Application Catalog website point  
- Asset Intelligence synchronization point  
- Certificate registration point  
- Cloud management gateway connection point  
- Data warehouse service point  
- Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection point  
- Enrollment point  
- Enrollment proxy point  
- Fallback status point  
- Management point
- Reporting services point  
- Service connection point  
- Site database server <sup>[Note 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software update point  
- State migration point

## <a name="bkmk_2016"></a> Windows Server 2016

*Applies to Windows Server 2016: Standard and Datacenter*

This OS version is supported for the following roles:

#### Site servers

- Central administration site  
- Primary site  
- Secondary site  

#### Site system servers

- Application Catalog web service point  
- Application Catalog website point  
- Asset Intelligence synchronization point  
- Certificate registration point  
- Cloud management gateway connection point  
- Data warehouse service point  
- Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection point  
- Enrollment point  
- Enrollment proxy point  
- Fallback status point  
- Management point
- Reporting services point  
- Service connection point  
- Site database server <sup>[Note 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software update point  
- State migration point

## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### Site system server

- Distribution point <sup>[Note 1](#bkmk_note1)</sup>  

## <a name="bkmk_2012r2"></a> Windows Server 2012 R2

*Applies to Windows Server 2012 R2: Standard and Datacenter*

#### Site servers

- Central administration site  
- Primary site  
- Secondary site  

#### Site system servers

- Application Catalog web service point  
- Application Catalog website point  
- Asset Intelligence synchronization point  
- Certificate registration point  
- Cloud management gateway connection point  
- Data warehouse service point  
- Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection point  
- Enrollment point  
- Enrollment proxy point  
- Fallback status point  
- Management point
- Reporting services point  
- Service connection point  
- Site database server <sup>[Note 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software update point  
- State migration point  

## <a name="bkmk_2012"></a> Windows Server 2012  

*Applies to Windows Server 2012: Standard and Datacenter*

#### Site servers

- Central administration site  
- Primary site  
- Secondary site  

#### Site system servers

- Application Catalog web service point  
- Application Catalog website point  
- Asset Intelligence synchronization point  
- Certificate registration point  
- Cloud management gateway connection point  
- Data warehouse service point  
- Distribution point <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection point  
- Enrollment point  
- Enrollment proxy point  
- Fallback status point  
- Management point
- Reporting services point  
- Service connection point  
- Site database server <sup>[Note 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Software update point  
- State migration point  

## <a name="bkmk_client"></a> Client OS versions

The following client OS versions are supported for use as a **distribution point** <sup>[Note 1](#bkmk_note1)</sup>:  

- Windows 10 (x86, x64): Pro and Enterprise

    For more information on supported build versions, see [Support for Windows 10](/configmgr/core/plan-design/configs/support-for-windows-10).

- Windows 8.1 (x86, x64): Professional and Enterprise

This support has the following limitation:  

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

## <a name="bkmk_core"></a> Server core installations

The server core installation of the following server OS versions are supported for use as a **distribution point**:

- Windows Server 2019 (starting in Configuration Manager, version 1810)  
- Windows Server, version 1809 (starting in Configuration Manager, version 1810)  
- Windows Server, version 1803 (starting in Configuration Manager, version 1802)  
- Windows Server, version 1709 (starting in Configuration Manager, version 1710)  
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

This support has the following limitation:  

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. Starting in version 1806, you can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

## General notes

### <a name="bkmk_note1"></a> Note 1: Distribution points

Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information, see [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

### <a name="bkmk_note2"></a> Note 2: Site database servers

Site database servers aren't supported on a read-only domain controller (RODC). For more information, see the Microsoft Support article: [You may encounter problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911). 

Additionally, secondary site servers aren't supported on any domain controller.  
