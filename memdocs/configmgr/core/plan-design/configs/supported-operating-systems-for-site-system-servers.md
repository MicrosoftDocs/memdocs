---
title: Supported site system servers
titleSuffix: Configuration Manager
description: Learn which Windows versions you can use to host a Configuration Manager site or site system role.
ms.date: 04/05/2021
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

- [Recommended hardware for Configuration Manager](recommended-hardware.md)
- [Site and site system prerequisites for Configuration Manager](site-and-site-system-prerequisites.md)
- [Size and scale numbers for Configuration Manager](size-and-scale-numbers.md)

## <a name="bkmk_2019"></a> Windows Server 2019

*Applies to Windows Server 2019: Standard and Datacenter* 

This OS version is supported for the following roles:

#### Site servers

- Central administration site  
- Primary site  
- Secondary site  

#### Site system servers

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

    For more information on supported build versions, see [Support for Windows 10](support-for-windows-10.md).

- Windows 8.1 (x86, x64): Professional and Enterprise

This support has the following limitation:  

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. You can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

## <a name="bkmk_core"></a> Server core installations

The server core installation of the following server OS versions are supported for use as a **distribution point**:

- Windows Server 2019
- Windows Server, version 1809
- Windows Server, version 1803
- Windows Server, version 1709
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

This support has the following limitation:  

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. You can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

## General notes

### <a name="bkmk_note1"></a> Note 1: Distribution points

Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information, see [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="bkmk_note2"></a> Note 2: Site database servers

Site database servers aren't supported on a read-only domain controller (RODC). For more information, see the Microsoft Support article: [You may encounter problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911). 

Additionally, secondary site servers aren't supported on any domain controller.  
