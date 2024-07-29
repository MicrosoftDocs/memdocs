---
title: Supported Configurations for the LTSB
titleSuffix: Configuration Manager
description: Understand what operating systems and dependent products work with the Long-Term Servicing Branch of System Center Configuration Manager.
ms.date: 10/11/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Supported Configurations for the Long-Term Servicing Branch of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Long-Term Servicing Branch)*

Use the information in this topic to understand what operating systems and product dependencies are supported by the Long-Term Servicing Branch (LTSB) of Configuration Manager.
If not stated otherwise in this or the LTSB specific topics, the same configurations and limitations that apply to the Current Branch version 1606 apply to the LTSB.  When conflicts occur, use the information that applies to the edition you are using. Typically, the LTSB is more limited than the Current Branch.

## General statement of support
The following products and technologies are supported by this branch of Configuration Manager. However, their inclusion in this content does not express an extension of support for any product or version beyond that product's individual support lifecycle. Products that are beyond their support lifecycle are not supported for use with Configuration Manager. For more information, visit the [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) website and read the Microsoft Support Lifecycle Policy FAQ.

Additionally, products and product versions that are not listed in the following topics are not supported unless they have been announced on the [Enterprise Mobility + Security Blog](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity).

**Limitations for future support:**
The LTSB has limited support for future server and client operating systems and product dependencies. The platforms list for the LTSB is fixed for the life of the release:

**Windows:**
- Only quality and security updates for Windows are supported.
- No support is added for current branches (CB), current branches for business (CBB), or LTSB of Windows 10.
- No support for new major versions of Windows Server.

**SQL Server:**
- Only quality and security updates, or minor upgrades like service packs, is supported for SQL Server.
- No support for new major versions of SQL Server.  

## Site systems and servers
The LTSB supports the use of the following Windows computer operating systems as site systems.  Each operating system has the same requirements and limitations as the same entry in [Supported operating systems for site system servers](../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  For example, the Server Core installation of Windows 2012 R2 must be an x64 version, is only supported to host a distribution point, and does not support PXE or Multicast.

**Supported operating systems:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- The Server Core installation of Windows Server 2012
- The Server Core installation of Windows Server 2012 R2

## Client management
The following sections identify the client operating systems that you can manage with the LTSB. The LTSB does not support the addition of new operating systems as supported clients.

### Windows computers
You can use the LTSB to manage the following Windows computer operating systems with the Configuration Manager client software that is included with Configuration Manager. For more information, see [How to deploy clients to Windows computers](../clients/deploy/deploy-clients-to-windows-computers.md).

**Supported operating systems:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Note 1)
- Windows Server 2012 (x64): Standard, Datacenter (Note 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- The Server Core installation of Windows Server 2012 R2 (x64) (Note 2)
- The Server Core installation of Windows Server 2012 (x64) (Note 2)

**(Note 1)** Datacenter releases are supported but not certified for Configuration Manager.  
**(Note 2)** To support client push installation, the computer that runs this operating system version must run the File Server role service for the File and Storage Services server role. For information about installing Windows features on a Server Core computer, see [Install Server Roles and Features on a Server Core Server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11)).

### Windows Embedded
You can use the LTSB to manage the following Windows Embedded devices by installing the client software on the device.  For more information, see [Planning for client deployment to Windows Embedded devices](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).

**Requirements and limitations:**  

-   All client features are supported on supported Windows Embedded systems that do not have write filters enabled.  

-   Clients that use one of the following are supported for all features except power management:  

    -   Enhanced Write Filters (EWF)    

    -   RAM File-Based Write Filters (FBWF)    

    -   Unified Write Filters (UWF)  

-   Before you can monitor detected malware on Windows Embedded devices based on Windows XP, you must install the Microsoft Windows WMI scripting package on the embedded device. Use Windows Embedded Target Designer to install this package. The *WBEMDISP.DLL* and *WBEMDISP.TLB* files must exist and be registered in the %windir%\System32\WBEM folder on the embedded device to ensure that detected malware is reported.  

**Supported operating systems:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    

## Exchange Server connector
 The LTSB supports limited management of devices that connect to your Exchange Server instance, without installing client software. For more information, see [Manage mobile devices with Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

 **Requirements and limitations:**  

-   Configuration Manager offers limited management for mobile devices. Limited management is available when you use the Exchange Server connector for Exchange Active Sync (EAS) capable devices that connect to a server running Exchange Server or Exchange Online.  

-   For more information about the management functions that Configuration Manager supports for mobile devices that the Exchange Server connector manages, see [Choose a device management solution for Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Supported versions of Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> The LTSB does not support the management of devices that connect through an online service, like Exchange Online (Microsoft 365).

## Configuration Manager console
The LTSB supports the following operating systems to run the Configuration Manager console. Each computer that hosts the console must have a minimum .NET Framework version of 4.5.2 except for Windows 10, which requires a minimum of .NET Framework 4.6.

**Supported operating systems:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise


## SQL Server versions supported for the site database and reporting point
The LTSB supports the following versions of SQL Server to host the site database and reporting point. For each supported version, the same configuration requirements and limitations that appear in [Support for SQL Server versions](../plan-design/configs/support-for-sql-server-versions.md) for the current branch apply to the LTSB.  This support includes the use of a SQL Server Always On failover cluster instance or an availability group.

**Supported versions:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## Support for Active Directory domains
All LTSB site systems must be members of a supported Windows Active Directory domain. Support for Active Directory domains has the same requirements and limitations as those that appear in [Support for Active Directory domains](../plan-design/configs/support-for-active-directory-domains.md), but is limited to the following domain functional levels:

**Supported levels:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## Additional support topics that apply to the Long-Term Servicing Branch
The information in the following Current Branch topics apply to the LTSB:
- [Size and scale numbers](../plan-design/configs/size-and-scale-numbers.md)
- [Site and site system prerequisites](../plan-design/configs/site-and-site-system-prerequisites.md)
- [High availability options](../servers/deploy/configure/high-availability-options.md)
- [Recommended hardware](../plan-design/configs/recommended-hardware.md)
- [Support for Windows features and networks](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Support for virtualization environments](../plan-design/configs/support-for-virtualization-environments.md)