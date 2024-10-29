---
title: Supported site system servers
titleSuffix: Configuration Manager
description: Learn which Windows versions you can use to host a Configuration Manager site or site system role.
ms.date: 12/01/2023
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Supported operating systems for Configuration Manager site system servers

*Applies to: Configuration Manager (current branch)*

This article details the Windows versions that you can use to host a Configuration Manager site or site system role.

## Windows Server 2022

_Applies to Datacenter: Azure Edition, Standard and Datacenter editions_

Site servers:

- Central administration site
- Primary site
- Secondary site

Site system servers:

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
- SMS Provider
- Software update point
- State migration point

## Windows Server 2019

_Applies to Standard and Datacenter editions_

Site servers:

- Central administration site
- Primary site
- Secondary site

Site system servers:

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
- SMS Provider
- Software update point
- State migration point

## Windows Server 2016

_Applies to Standard and Datacenter editions_

Site servers:

- Central administration site
- Primary site
- Secondary site

Site system servers:

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
- SMS Provider
- Software update point
- State migration point

## Windows Storage Server 2016

Site system server:

- Distribution point <sup>[Note 1](#bkmk_note1)</sup>

## Windows Server 2012/2012 R2

_Applies to Standard and Datacenter_ 

On October 10th, 2023, Windows Server 2012 and Windows Server 2012 R2 entered the Extended Support Updates phase. Microsoft will no longer provide support for Configuration Manager site servers or roles installed to these Operating Systems. For more information, see [Extended Security Updates and Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!TIP]
>
> Starting in Configuration Manager 2309, you'll be notified when performing a site upgrade about site systems with operating systems that are past the end of support date. 
>
> Starting in Configuration Manager 2403 you'll be blocked from performing a site upgrade if any site systems are detected with operating systems that are past the end of support date. For more information, see [Extended Security Updates and Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

## Client OS versions

The following client OS versions are supported for use as a **distribution point** <sup>[Note 1](#bkmk_note1)</sup>:

- Windows 11 

    For more information on supported build versions and editions, see [Support for Windows 11](support-for-windows-11.md).

- Windows 10 (x86, x64)

    For more information on supported build versions and editions, see [Support for Windows 10](support-for-windows-10.md).

This support has the following limitation:

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. You can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

## Server core installations

The server core installation of the following server OS versions is supported for use as a **distribution point**:

- Windows Server 2022
- Windows Server 2019
- Windows Server, version 1809
- Windows Server, version 1803
- Windows Server, version 1709
- Windows Server 2016

This support has the following limitation:

- Distribution points on this OS don't support PXE or multicast with the default Windows Deployment Services. You can PXE-enable a distribution point on this OS with the option to **Enable a PXE responder without Windows Deployment Service**. For more information, see [Install and configure distribution points](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

## General notes

### Extended Security Updates for Windows Server 2012 and Windows Server 2012 R2

On October 10th, 2023, Windows Server 2012 and Windows Server 2012 R2 will enter the Extended Support Updates phase. Microsoft will no longer provide support for Configuration Manager site servers or roles installed to these Operating Systems. For more information, see [Extended Security Updates and Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

### <a name="bkmk_note1"></a> Note 1: Distribution points

Distribution points support several different configurations that each have different requirements. In some cases, these configurations support installation not only on servers, but on client operating systems. For more information, see [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).

### <a name="bkmk_note2"></a> Note 2: Site database servers

Site database servers aren't supported on a read-only domain controller (RODC). For more information, see [SQL Server security considerations: Installing SQL Server on a domain controller](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#Install_DC).

Additionally, secondary site servers aren't supported on any domain controller.

## Next steps

[Supported SQL Server versions](support-for-sql-server-versions.md)

See also:

- [Recommended hardware](recommended-hardware.md)
- [Site and site system prerequisites](site-and-site-system-prerequisites.md)
- [Size and scale numbers](size-and-scale-numbers.md)
