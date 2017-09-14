---
title: "Supported clients and devices | Microsoft Docs"
description: "Learn which operating systems System Center Configuration Manager supports for clients and devices."
ms.custom: na
ms.date: 8/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: arob98
ms.author: angrobe
manager: angrobe
---
# Supported operating systems for clients and devices for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager supports installing client software on a variety of Windows, Mac, Linux, and UNIX computers.  

 **Requirements and limitations for all clients:**  

-   Changing the startup type or **Log on as** settings for any Configuration Manager service is not supported and can prevent key services from running correctly.    

-   Installing or running the Configuration Manager client for Linux or UNIX or the client for Mac on computers under an account other than root is not supported. Doing so can prevent key services from running correctly.  

##  Windows computers  
 You can use the Configuration Manager client that is included with Configuration Manager to manage the following Windows operating systems. For more information, see [How to deploy clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

**Supported operating systems:**  


-  **Windows Server 2016**: Standard, Datacenter <sup>1</sup>
  - This operating system is supported beginning with Configuration Manager version 1606, with the hotfix rollup from KB3186654 (or the baseline version of 1606, which was released in October 2016).  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 with SP1** (x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise    

-   **Windows  Server 2008 with SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows 10**
   See [Support for versions of Windows 10](/sccm/core/plan-design/configs/support-for-windows-10) for details about the different release versions of Windows 10 that are supported by the different versions of Configuration Manager.

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **Windows 8** (x86, x64): Professional, Enterprise    

-   **Windows 7 with SP1** (x86, x64): Professional, Enterprise, and Ultimate    

-   **The Server Core installation of Windows Server 2016** (x64) <sup>2</sup>
  - This operating system is supported beginning with version 1606 with the hotfix rollup from KB3186654 (or the baseline version of 1606, which was released in October of 2016).


-   **The Server Core installation of Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **The Server Core installation of Windows Server 2012** (x64) <sup>2</sup>    

-   **The Server Core installation of Windows Server 2008 R2**  
    **(with no service pack, or with SP1)** (x64)    

-   **The Server Core installation of Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> Datacenter releases are supported but not certified for Configuration Manager. Hotfix support is not offered for issues that are specific to Windows Server Datacenter Edition.  

 <sup>2</sup> To support client push installation, the computer that runs this operating system version must run the File Server role service for the File and Storage Services server role. For information about installing Windows features on a Server Core computer, see [Install Server Roles and Features on a Server Core Server](http://go.microsoft.com/fwlink/p/?LinkId=299359) in the Windows Server 2012 TechNet library.  


##  Windows Embedded computers  
 You can manage Windows Embedded devices by installing Configuration Manager client software on the device.  For more information, see [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

**Requirements and limitations:**  

-   All client features are supported on Windows Embedded systems that do not have write filters enabled.  

-   Clients that use one of the following are supported for all features except power management:  

    -   Enhanced Write Filters (EWF)    

    -   RAM File-Based Write Filters (FBWF)    

    -   Unified Write Filters (UWF)  

-   The Application Catalog is not supported for any Windows Embedded device.  

-   Before you can monitor detected malware on Windows Embedded devices that are based on Windows XP, you must install the Microsoft Windows WMI scripting package on the device. Use Windows Embedded Target Designer to install this package.
The files **WBEMDISP.DLL** and **WBEMDISP.TLB** must exist and be registered in the folder **%windir%\System32\WBEM** on the embedded device to ensure that detected malware is reported.  

**Supported operating systems:**  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Embedded 8 Pro** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 with SP1** (x86, x64)    

The following operating systems are based on Windows XP Embedded, and only supported with Configuration Manager version 1610 and earlier. [Beginning with version 1702, these embedded operating systems are no longer supported](/sccm/core/plan-design/changes/removed-and-deprecated-features#client-operating-systems).  

-   **WEPOS 1.1 with SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## Windows CE computers
 You can manage Windows CE devices with the Configuration Manager mobile device legacy client that is included with Configuration Manager.  

**Requirements and limitations**  

-   The mobile device client requires 0.78 MB of storage space for installation. Sign-in can require up to 256 KB of additional storage space.    

-   Features for these mobile devices vary by platform and client type. For information about which management functions are supported, see [Choose a device management solution for System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

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

## Mac computers  
 You can manage Mac OS X computers with the Configuration Manager client for Mac.  

 The Mac client installation package is not supplied with the Configuration Manager media. Download the **Clients for Additional Operating Systems** from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

 For more information, see [How to deploy clients to Macs in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-macs.md).  

**Supported versions:**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra )

##  Linux and UNIX servers  
 You can manage Linux and UNIX servers with the Configuration Manager client for Linux and UNIX.  

 The Linux and UNIX client installation packages are  are not supplied with the Configuration Manager media. Download the **Clients for Additional Operating Systems** from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184). In addition to client installation packages, the client download includes the script that manages the installation of the client on each computer.  

**Requirements and limitations:**  

-   To review operating system file dependencies for the client for Linux and UNIX, see [Prerequisites for Client Deployment to Linux and UNIX Servers](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

-   For an overview of supported management capabilities for Linux or UNIX, see [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   For supported versions of Linux and UNIX, the listed version includes all subsequent minor versions. For example,  CentOS version 6 includes  CentOS 6.3. Similarly, support for an operating system that uses service packs (such as SUSE Linux Enterprise Server 11 SP1) includes subsequent service packs for that operating system version.  

-   For information about client installation packages and the Universal Agent, see [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

**Supported versions:** The following versions are supported by using the indicated .tar file.  

### AIX  

|||  
|-|-|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### CentOS  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### Debian  

|||  
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

|||  
|-|-|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

### Oracle Linux  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### Solaris  

|||  
|-|-|  
|Version 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Version 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### Ubuntu  

|||  
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  


##  Mobile devices enrolled by Microsoft Intune  
 For details about the computers and devices that you can manage when you integrate Microsoft Intune with Configuration Manager, see the following two topics   in the Microsoft Intune documentation library:  

-   [Mobile device management capabilities in Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Windows PC management capabilities in Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="bkmk_OnpremOS"></a> On-premises mobile device management  
 Configuration Manager has built-in capabilities for managing devices that are on-premises without installing client software.  For more information, see [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Requirements and limitations:**  

-   You must configure the **Service connection point** at the top-tier site of your hierarchy.  

**Supported operating systems:**  

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

- **Windows 10 IoT Mobile Enterprise**

- **Windows 10 Team for Surface Hub**

##  <a name="bkmk_ExSrvConOS"></a> Exchange Server connector  
Configuration Manager supports limited management of devices that connect to your Exchange Server, without installing the Configuration Manager client. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Requirements and limitations:**  

-   Configuration Manager offers limited management for mobile devices when you use devices with Exchange Server connector for Exchange Active Sync that connect to a server that's running Exchange Server or Exchange Online.  

-   For more information about which management functions Configuration Manager supports for mobile devices that the Exchange Server connector manages, see Determine How to Manage Mobile Devices in Configuration Manager.  

**Supported versions of Exchange Server:**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)**: This includes Business Productivity Online Standard Suite  
