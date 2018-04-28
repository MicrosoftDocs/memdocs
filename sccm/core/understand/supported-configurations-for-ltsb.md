---
title: "Supported Configurations for the LTSB "
titleSuffix: "Configuration Manager"
description: "Understand what operating systems and dependent products work with the Long-Term Servicing Branch of System Center Configuration Manager."
ms.date: 5/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Supported Configurations for the Long-Term Servicing Branch of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Long-Term Servicing Branch)*

Use the information in this topic to understand what operating systems and product dependencies are supported by the Long-Term Servicing Branch (LTSB) of Configuration Manager.
If not stated otherwise in this or the LTSB specific topics, the same configurations and limitations that apply to the Current Branch version 1606 apply to the LTSB.  When conflicts occur, use the information that applies to the edition you are using. Typically, the LTSB is more limited than the Current Branch.

## General statement of support
The following products and technologies are supported by this branch of Configuration Manager. However, their inclusion in this content does not express an extension of support for any product or version beyond that product's individual support lifecycle. Products that are beyond their support lifecycle are not supported for use with Configuration Manager. For more information, visit the [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270) website and read the [Microsoft Support Lifecycle Policy FAQ](http://go.microsoft.com/fwlink/p/?LinkId=31976).

Additionally, products and product versions that are not listed in the following topics are not supported unless they have been announced on the [Enterprise Mobility + Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/).

**Limitations for future support:**
The LTSB has limited support for future server and client operating systems and product dependencies. The platforms list for the LTSB is fixed for the life of the release:

**Windows:**
- Only quality and security updates for Windows are supported.
- No support is added for current branches (CB), current branches for business (CBB), or LTSB of Windows 10.
-	No support for new major versions of Windows Server.

**SQL Server:**
- Only quality and security updates, or minor upgrades like service packs, is supported for SQL Server.
- No support for new major versions of SQL Server.  

## Site systems and servers
The LTSB supports the use of the following Windows computer operating systems as site systems.  Each operating system has the same requirements and limitations as the same entry in [Supported operating systems for site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  For example, the Server Core installation of Windows 2012 R2 must be an x64 version, is only supported to host a distribution point, and does not support PXE or Multicast.

**Supported operating systems:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 with SP1 (x64): Standard, Enterprise, Datacenter
- Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise, Datacenter  *(See note 1)*
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 with SP1 (x86, x64): Professional, Enterprise, Ultimate
- The Server Core installation of Windows Server 2012
- The Server Core installation of Windows Server 2012 R2    

*Note 1*: This operating system is not supported for site servers or site system roles with the exception of the distribution point and pull-distribution point. You can continue to use this operating system as a distribution point until deprecation of this support is announced, or this operating system's extended support period expires. For more information, see [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095).

## Client management
The following sections identify the client operating systems that you can manage with the LTSB. The LTSB does not support the addition of new operating systems as supported clients.

### Windows computers
You can use the LTSB to manage the following Windows computer operating systems with the Configuration Manager client software that is included with Configuration Manager. For more information, see [How to deploy clients to Windows computers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Supported operating systems:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Note 1)
- Windows Server 2012 (x64): Standard, Datacenter (Note 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 with SP1 (x64): Standard, Enterprise, Datacenter (Note 1)
- Windows Storage Server 2008 R2 (x86, x64): Workgroup, Standard, Enterprise
- Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise, Datacenter (Note 1)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 with SP1 (x86, x64): Professional, Enterprise, Ultimate
- The Server Core installation of Windows Server 2012 R2 (x64) (Note 2)
- The Server Core installation of Windows Server 2012 (x64) (Note 2)
- The Server Core installation of Windows Server 2008 R2 SP1 (x64)
- The Server Core installation of Windows Server 2008 SP2 (x86, x64)

**(Note 1)** Datacenter releases are supported but not certified for Configuration Manager.  
**(Note 2)** To support client push installation, the computer that runs this operating system version must run the File Server role service for the File and Storage Services server role. For information about installing Windows features on a Server Core computer, see [Install Server Roles and Features on a Server Core Server](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx) in the Windows Server 2012 TechNet library.

### Windows Embedded
You can use the LTSB to manage the following Windows Embedded devices by installing the client software on the device.  For more information, see [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).

**Requirements and limitations:**  

-   All client features are supported on supported Windows Embedded systems that do not have write filters enabled.  

-   Clients that use one of the following are supported for all features except power management:  

    -   Enhanced Write Filters (EWF)    

    -   RAM File-Based Write Filters (FBWF)    

    -   Unified Write Filters (UWF)  

-   The Application Catalog is not supported for any Windows Embedded device.  

-   Before you can monitor detected malware on Windows Embedded devices based on Windows XP, you must install the Microsoft Windows WMI scripting package on the embedded device. Use Windows Embedded Target Designer to install this package. The *WBEMDISP.DLL* and *WBEMDISP.TLB* files must exist and be registered in the %windir%\System32\WBEM folder on the embedded device to ensure that detected malware is reported.  

**Supported operating systems:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 with SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### Windows CE  
 You can manage Windows CE devices with the Configuration Manager mobile device legacy client that is included with Configuration Manager.  

**Requirements and limitations:**  

-   The mobile device client requires 0.78 MB of storage space to install the client. A mobile device can require up to 256 KB of additional storage space to sign in.    

-   Features for these mobile devices vary by platform and client type. For information about the kind of management functions that Configuration Manager supports for a mobile device legacy client, see [Choose a device management solution for System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Supported operating systems:**  

-   Windows CE 7.0 (ARM and x86 processors)  

**Supported languages include:**  
-   Chinese (simplified and traditional)    
-   English (US)    
-   French (France)    
-   German    
-   Italian    
-   Japanese  
-   Korean  
-   Portuguese (Brazil)  
-   Russian  
-   Spanish (Spain)  

### Mac computers  
 You can use the LTSB to manage Mac OS X computers with the Configuration Manager client for Mac.

The Mac client installation package is not supplied with the Configuration Manager media. You can download it as part of the "Clients for Additional Operating Systems" download from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

Support for Mac operating systems is limited to those listed in this section. Support does not include additional operating systems that might be supported by a future update to Mac client installation packages for Current Branch.

For more information, see [How to deploy clients to Macs in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs).

**Supported versions:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## Linux and UNIX servers
You can use the LTSB to manage Linux and UNIX servers with the Configuration Manager client for Linux and UNIX.

The Linux and UNIX client installation packages are not supplied with the Configuration Manager media. You can download them as part of the "Clients for Additional Operating Systems" download from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184). In addition to client installation packages, the client download includes the install script that manages the installation of the client on each computer.

Support for Linux and UNIX operating systems is limited to those listed in this section. Support does not include additional operating systems that might be supported by a future update to Linux and UNIX client packages for Current Branch.

**Requirements and limitations:**  

-   To review operating system file dependencies for the client for Linux and UNIX, see [Prerequisites for Client Deployment to Linux and UNIX Servers](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu).  
-   For an overview of the management capabilities supported for computers that run Linux or UNIX, see [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   For supported versions of Linux and UNIX, the listed version includes all subsequent minor versions. For example, where support is indicated for CentOS version 6, this also includes any subsequent minor version of CentOS 6, such as CentOS 6.3. Similarly, when support is listed for an operating system that uses service packs, such as SUSE Linux Enterprise Server 11 SP1, support includes subsequent service packs for that operating system version.
-   For information about client installation packages and the Universal Agent, see [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Supported versions:**   
The following versions are supported by using the indicated .tar file.  
### AIX  

|Version|File|  
|-|-|  
|Version 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### CentOS  

|Version|File|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### Debian  

|Version|File|    
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 8 x64|ccm-Universalx64.&lt;build\>.tar|  

### HP-UX  

|Version|File|  
|-|-|  
|Version 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Version 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Version 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### Oracle Linux  

|Version|File|    
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### Red Hat Enterprise Linux (RHEL)  

|Version|File|  
|-|-|  
|Version 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Version 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### Solaris  

|Version|File|   
|-|-|  
|Version 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Version 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Version 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### SUSE Linux Enterprise Server (SLES)  

|Version|File|  
|-|-|  
|Version 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### Ubuntu  

|Version|File|    
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

### Exchange Server connector
 The LTSB supports limited management of devices that connect to your Exchange Server instance, without installing client software. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Requirements and limitations:**  

-   Configuration Manager offers limited management for mobile devices. Limited management is available when you use the Exchange Server connector for Exchange Active Sync (EAS) capable devices that connect to a server running Exchange Server or Exchange Online.  

-   For more information about the management functions that Configuration Manager supports for mobile devices that the Exchange Server connector manages, see [Choose a device management solution for System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Supported versions of Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> The LTSB does not support the management of devices that connect through an online service, like Exchange Online (Office 365).


## Configuration Manager console
The LTSB supports the following operating systems to run the Configuration Manager console. Each computer that hosts the console must have a minimum .NET Framework version of 4.5.2 except for Windows 10, which requires a minimum of .NET Framework 4.6.

**Supported operating systems:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 with SP1 (x64): Standard, Enterprise, Datacenter
- Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 with SP1 (x86, x64): Professional, Enterprise, Ultimate


## SQL Server versions supported for the site database and reporting point
The LTSB supports the following versions of SQL Server to host the site database and reporting point. For each supported version, the same configuration requirements and limitations that appear in [Support for SQL Server versions](/sccm/core/plan-design/configs/support-for-sql-server-versions) for the Current Branch apply to the LTSB.  This includes the use of a SQL Server Cluster, or a SQL Server AlwaysOn availability group.  

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
All LTSB site systems must be members of a supported Windows Active Directory domain. Support for Active Directory domains has the same requirements and limitations as those that appear in [Support for Active Directory domains](/sccm/core/plan-design/configs/support-for-active-directory-domains), but is limited to the following domain functional levels:

**Supported levels:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## Additional support topics that apply to the Long-Term Servicing Branch
The information in the following Current Branch topics apply to the LTSB:
- [Size and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [High availability options](/sccm/protect/understand/high-availability-options)
- [Recommended hardware](/sccm/core/plan-design/configs/recommended-hardware)
- [Support for Windows features and networks](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Support for virtualization environments](/sccm/core/plan-design/configs/support-for-virtualization-environments)
