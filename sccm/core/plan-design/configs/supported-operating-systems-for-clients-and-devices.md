---
title: Supported clients and devices
titleSuffix: Configuration Manager
description: Learn which OS versions Configuration Manager supports for clients and devices.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Supported OS versions for clients and devices for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager supports installing client software on Windows and macOS computers.  

## General requirements and limitations

Review the following requirements and limitations for all clients:

- Changing the startup type or **Log on as** settings for any Configuration Manager service isn't supported. This change can prevent key services from running correctly.


## Windows computers  

To manage the following Windows OS versions, use the client that's included with Configuration Manager. For more information, see [How to deploy clients to Windows computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).  

### Supported client OS versions

- **Windows 10**  

    For more detailed information, see [Support for Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

- **Windows 8.1** (x86, x64): Professional, Enterprise

- **Windows 7 with SP1** (x86, x64): Professional, Enterprise, and Ultimate

#### Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) is a preview feature of Microsoft Azure and Microsoft 365. Starting in version 1906, use Configuration Manager to manage these virtual devices running Windows in Azure.

Similar to a terminal server, these virtual devices allow multiple concurrent active user sessions. To help with client performance, Configuration Manager now disables user policies on any device that allows these multiple user sessions. Even if you enable user policies, the client disables them by default on these devices, which include Windows Virtual Desktop and terminal servers.

The client only disables user policy when it detects this type of device during a new installation. For an existing client of this type that you update to this version, the previous behavior persists. On an existing device, it configures the user policy setting even if it detects that the device allows multiple user sessions.

If you require user policy in this scenario, and accept any potential performance impact, use the Configuration Manager SDK with the [SMS_PolicyAgentConfig server WMI class](/sccm/develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class). Set the new `PolicyEnableUserPolicyOnTS` property to `true`.

> [!Note]  
> You can't use co-management with a Windows Virtual Desktop. Windows 10 Enterprise for Virtual Desktop (EVD) is actually a Windows Server edition, which doesn't have the MDM components.<!-- SCCMDocs-pr#3950 -->

### Supported server OS versions

- **Windows Server 2019**: Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>  
    (Starting with Configuration Manager version 1806.)

- **Windows Server 2016**: Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: Workgroup, Standard  

- **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

- **Windows Server 2008 R2 with SP1** (x64): Standard, Enterprise, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise

- **Windows Server 2008 with SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

#### Server Core

The following versions specifically refer to the Server Core installation of the OS. <sup>[Note 3](#bkmk_note3)</sup>  

Windows Server semi-annual channel versions are Server Core installations, such as Windows Server, version 1809. As a Configuration Manager client, they're supported the same as the associated Windows 10 semi-annual channel version. For more information, see [Support for Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).

- **Windows Server 2019** (x64) <sup>[Note 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[Note 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[Note 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[Note 2](#bkmk_note2)</sup>

- **Windows Server 2008 R2** with no service pack, or with SP1 (x64)

- **Windows Server 2008 SP2** (x86, x64)

#### <a name="bkmk_note1"></a> Note 1

Configuration Manager tests and supports Windows Server Datacenter editions, but isn't officially certified for Windows Server. Configuration Manager hotfix support isn't offered for issues that are specific to Windows Server Datacenter Edition. For more information on the Windows Server certification program, see [Windows Server Catalog](https://www.windowsservercatalog.com/).

#### <a name="bkmk_note2"></a> Note 2

To support [client push installation](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation), add the File Server service of the File and Storage Services server role. For more information about installing Windows features on Server Core, see [Install roles, role services, and features by using Windows PowerShell cmdlets](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).  

#### <a name="bkmk_note3"></a> Note 3

The new Software Center app isn't supported on any version of Windows Server Core.<!--SCCMDocs issue 683-->


## Windows Embedded computers  

Manage Windows Embedded devices by installing the Configuration Manager client on the device. For more information, see [Planning for client deployment to Windows Embedded devices](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).  

### Requirements and limitations

- All client features are supported on Windows Embedded systems that don't have write filters enabled.  

- Clients that use one of the following are supported for all features except power management:  

    - Enhanced Write Filters (EWF)

    - RAM File-Based Write Filters (FBWF)

    - Unified Write Filters (UWF)  

- The application catalog isn't supported for any Windows Embedded device.  

### Supported OS versions  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    This version includes the long-term servicing channel (LTSC). For more information, see [Overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 with SP1** (x86, x64)


## Windows CE computers

Manage Windows CE devices with the Configuration Manager mobile device legacy client that is included with Configuration Manager.  

### Requirements and limitations

- The mobile device client requires 0.78 MB of storage space for installation. Sign-in can require up to 256 KB of additional storage space.

- Features for these mobile devices vary by platform and client type. For information about which management functions are supported, see [Choose a device management solution](/sccm/core/plan-design/choose-a-device-management-solution).  

### Supported OS versions

- Windows CE 7.0 (ARM and x86 processors)  

    > [!Note]
    > Support is deprecated for Windows CE 7.0 in Configuration Manager. For more information, see [Removed and deprecated items for Configuration Manager clients](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client).

#### Supported languages include

- Chinese (simplified and traditional)

- English (US)

- French (France)

- German

- Italian

- Japanese  

- Korean  

- Portuguese (Brazil)  

- Russian  

- Spanish (Spain)  

## <a name="bkmk_ESU"></a> Extended Security Updates and Configuration Manager

The [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) program is a last resort option for customers who need to run certain legacy Microsoft products past the end of support. It includes Critical and/or Important security updates (as defined by the [Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc)) for a maximum of three years after the product’s End of Extended Support date.

Products that are beyond their support lifecycle aren't supported for use with Configuration Manager. This includes any products that are covered under the ESU program. Security updates released under the ESU program will be published to Windows Server Update Services (WSUS). These updates will appear in the Configuration Manager console. While products that are covered under the ESU program are no longer supported for use with Configuration Manager, the [latest released version of Configuration Manager current branch](/sccm/core/servers/manage/updates#version-details) can be used to deploy and install Windows security updates released under the program. The latest released version can also be used to deploy supported OSes via operating system deployment (OSD).

Client management features not related to Windows software update management or OSD will no longer be tested on the operating systems covered under the ESU program and we don't guarantee that they'll continue to function. It's highly recommended to upgrade or migrate to a current version of the operating systems as soon as possible to receive client management support.

## Mac computers  

Manage Apple Mac computers with the Configuration Manager client for macOS.  

The macOS client installation package isn't supplied with the Configuration Manager media. Download the **Clients for Additional Operating Systems** from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719).  

For more information, see [How to deploy clients to Macs](/sccm/core/clients/deploy/deploy-clients-to-macs).  

### Requirements and limitations

- Installing or running the Configuration Manager client for macOS on computers under an account other than root isn't supported. Doing so can prevent key services from running correctly.  

### Supported versions

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

- **macOS Sierra (10.12)**

- **macOS 10.11** (El Capitan)  

- **macOS 10.10** (Yosemite)  

- **macOS 10.9** (Mavericks)

- **macOS 10.8** (Mountain Lion)

- **macOS 10.7** (Lion)

- **macOS 10.6** (Snow Leopard)


## Linux and UNIX servers  

> [!Important]  
> Configuration Manager version 1902 drops support for Linux and UNIX as a client. Deprecation was announced with [version 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support). Consider Microsoft Azure Management for managing Linux servers. Azure solutions have extensive Linux support that in most cases exceed Configuration Manager functionality, including end-to-end patch management for Linux.

The Linux and UNIX client installation packages aren't supplied with the Configuration Manager media. Download the **Clients for Additional Operating Systems** from the [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184). In addition to client installation packages, the client download includes the script that manages the installation of the client on each computer.  

### Requirements and limitations

- To review OS file dependencies for the client for Linux and UNIX, see [Prerequisites for client deployment to Linux and UNIX servers](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU).  

- For an overview of supported management capabilities for Linux or UNIX, see [How to deploy clients to UNIX and Linux servers](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  

- For supported versions of Linux and UNIX, the listed version includes all subsequent minor versions. For example, CentOS version 6 includes  CentOS 6.3. Similarly, support for an OS that uses service packs (such as SUSE Linux Enterprise Server 11 SP1) includes subsequent service packs for that OS version.  

- For information about client installation packages and the Universal Agent, see [How to deploy clients to UNIX and Linux servers](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  

### Supported versions

The following versions are supported by using the indicated .tar file.  

#### AIX  

|Version|TAR file|  
|-|-|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

#### CentOS  

|Version|TAR file|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### Debian  

|Version|TAR file|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### HP-UX  

|Version|TAR file|  
|-|-|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### Oracle Linux  

|Version|TAR file|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### Red Hat Enterprise Linux (RHEL)  

|Version|TAR file|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### Solaris  

|Version|TAR file|  
|-|-|  
|Version 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Version 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### SUSE Linux Enterprise Server (SLES)  

|Version|TAR file|  
|-|-|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### Ubuntu  

|Version|TAR file|  
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  


## <a name="bkmk_OnpremOS"></a> On-premises MDM

Configuration Manager has built-in capabilities for managing mobile devices that are on-premises without installing client software. For more information, see [Manage mobile devices with on-premises infrastructure](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

### Requirements and limitations

- Configure the **Service connection point** at the top-tier site of your hierarchy.  

### Supported operating systems

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    This version includes the long-term servicing channel (LTSC). For more information, see [Overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team for Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!Note]
    > Support is deprecated for Windows 10 Mobile and Windows 10 Mobile Enterprise in Configuration Manager. For more information, see [Removed and deprecated items for Configuration Manager clients](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client).


## <a name="bkmk_ExSrvConOS"></a> Exchange Server connector  

Configuration Manager supports limited management of devices that connect to your Exchange Server, without installing the Configuration Manager client. For more information, see [Manage mobile devices with Configuration Manager and Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

### Supported versions of Exchange Server

- **Exchange Online (Office 365)**: This version includes Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** or **Exchange Server 2010 SP2**
