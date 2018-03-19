---
title: OSD infrastructure requirements
titleSuffix: Configuration Manager
description: Learn the external and product dependencies and requirements for operating system deployment
ms.custom: na
ms.date: 03/21/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: 24
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Infrastructure requirements for OS deployment in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

OS deployment in Configuration Manager has external dependencies as well as dependencies within the product. Use this article to help you prepare the infrastructure for OS deployment.  



##  <a name="BKMK_ExternalDependencies"></a> Dependencies external to Configuration Manager  
 This section provides information about external tools, installation kits, and OS versions that are required to deploy operating systems in Configuration Manager.  

### Windows ADK for Windows 10  
 The Windows Assessment and Deployment Kit (ADK) is a set of tools and documentation that support the configuration and deployment of Windows. Configuration Manager uses the Windows ADK to automate actions such as installing Windows, capturing images, and migrating user profiles and data.  

 The following features of the Windows ADK must be installed on the site server of the top-level site in the hierarchy, on the site server of each primary site in the hierarchy, and on the SMS Provider site system server:  

-   User State Migration Tool (USMT) <sup>1</sup>  

-   Windows Deployment Tools  

-   Windows Preinstallation Environment (Windows PE)

For a list of the versions of the Windows 10 ADK that you can use with different versions of Configuration Manager, see [Support For Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> USMT isn't required on the SMS Provider site system server.  

> [!NOTE]  
>  You must manually install the Windows ADK on each site server before you install the Configuration Manager site.  

 For more information, see:  

-   [Windows ADK for Windows 10 scenarios for IT Pros](/windows/deployment/windows-adk-scenarios-for-it-pros)  

-   [Download the Windows ADK for Windows 10](/windows-hardware/get-started/adk-install)  

-   [Support for Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### User State Migration Tool (USMT)  
 Configuration Manager uses a USMT package that includes the USMT 10 source files to capture and restore the user state as part of your OS deployment. Configuration Manager setup at the top-level site automatically creates the USMT package. USMT 10 captures user state from Windows 7, Windows 8, Windows 8.1, and Windows 10.  

 For more information, see:  

-   [Common Migration Scenarios for USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

-   [Manage user state](../get-started/manage-user-state.md)  

### Windows PE  
 Windows PE is used for boot images to start a computer. It's a Windows version with limited services that is used during the pre-installation and deployment of Windows. The following list includes the supported versions of the Windows ADK for Configuration Manager, current branch:  

-   **Windows ADK version**  

     Windows ADK for Windows 10. For more information, see [Support For Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

-   **Windows PE versions for boot images customizable from the Configuration Manager console**  

     Windows PE 10  

-   **Supported Windows PE versions for boot images not customizable from the Configuration Manager console**  

     Windows PE 3.1<sup>1</sup> and Windows PE 5  

     <sup>1</sup> You can only add a boot image to Configuration Manager when it is based on Windows PE 3.1. Install the Windows AIK Supplement for Windows 7 SP1 to upgrade Windows AIK for Windows 7 (based on Windows PE 3) with the Windows AIK Supplement for Windows 7 SP1 (based on Windows PE 3.1). You can download Windows AIK Supplement for Windows 7 SP1 from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

     For example, when you have Configuration Manager, you can customize boot images from Windows ADK for Windows 10 (based on Windows PE 10) from the Configuration Manager console. However, while boot images based on Windows PE 5 are supported, you must customize them from a different computer and use the version of DISM that is installed with Windows ADK for Windows 8. Then, you can add the boot image to the Configuration Manager console. For more information with the steps to customize a boot image (add optional components and drivers), enable command support to the boot image, add the boot image to the Configuration Manager console, and update distribution points with the boot image, see [Customize boot images](../get-started/customize-boot-images.md). For more information about boot images, see [Manage boot images](../get-started/manage-boot-images.md).  


### Windows Server Update Services (WSUS)  
 WSUS is required for the software update point, which is required to install software updates during OS deployment. For more information, see [Install a configure a software update point](/sccm/sum/get-started/install-a-software-update-point).


### Internet Information Services (IIS) on the site system servers  
 IIS is required for the distribution point, state migration point, and management point. For more information, see [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


### Windows Deployment Services (WDS)  
 WDS is needed for PXE deployments and when you use multicast to optimize bandwidth in your deployments. For more information, see [Windows Deployment Services](#BKMK_WDS) in this article.  


### Dynamic Host Configuration Protocol (DHCP)  
 DHCP is required for PXE deployments. You must have a functioning DHCP server with an active host to deploy operating systems by using PXE. For more information about PXE deployments, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### Supported operating systems and hard disk configurations  
 For more information about the operating system versions and hard disk configurations that are supported by Configuration Manager when you deploy operating systems, see [Supported operating systems](#BKMK_SupportedOS) and [Supported disk configurations](#BKMK_SupportedDiskConfig).  


### Windows device drivers  
 Windows device drivers can be used when you install the OS on the destination computer. They are also used when you run Windows PE in a boot image. For more information, see [Manage drivers](../get-started/manage-drivers.md).  



##  <a name="BKMK_InternalDependencies"></a> Configuration Manager dependencies  
 This section provides information about Configuration Manager OS deployment prerequisites.  


### OS image  
 OS images in Configuration Manager are stored in the Windows Imaging (WIM) file format. They represent a compressed collection of reference files and folders. These images are required to successfully install and configure an OS on a computer. For more information, see [Manage operating system images](../get-started/manage-operating-system-images.md).  


### Driver catalog  
 To deploy a device driver, you must import the device driver, enable it, and make it available on a distribution point that the Configuration Manager client can access. For more information about the driver catalog, see [Manage drivers](../get-started/manage-drivers.md).  


### Management point  
 Management points transfer information between clients and the Configuration Manager site. The client uses a management point to run the task sequence to complete the OS deployment. For more information about task sequences, see [Planning considerations for automating tasks](planning-considerations-for-automating-tasks.md).  


### Distribution point  
 Distribution points are used in most deployments to store the data that is used to deploy an OS, such as the image or driver packages. Task sequences typically retrieve data from a distribution point to deploy the OS. For more information about how to install distribution points and manage content, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### PXE-enabled distribution point  
 To deploy PXE-initiated deployments, you must configure a distribution point to accept PXE requests from clients. For more information, see [Configure a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).


### Multicast-enabled distribution point  
 To optimize your OS deployments by using multicast, you must configure a distribution point to support multicast. For more information, see [Configure a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   


### State migration point  
 When you capture and restore user state data for side-by-side and refresh deployments, you must configure a state migration point to store the user state data on another computer.  

 For more about how to configure the state migration point, see [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 For information about how to capture and restore user state, see [Manage user state](../get-started/manage-user-state.md).  


### Reporting services point  
 To use Configuration Manager reports for OS deployments, you must install and configure a reporting services point. For more information, see [Reporting](../../core/servers/manage/reporting.md).  


### Security permissions for OS deployments  
 The **Operating System Deployment Manager** security role is a built-in role that you can't change. However, you can copy the role, make changes, and then save these changes as a new custom security role. Here are some of the permissions that apply directly to OS deployments:  

-   **Boot Image Package**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope  

-   **Device Drivers**: Create, Delete, Modify, Modify Folder, Modify Report, Move Object, Read, Run Report  

-   **Driver Package**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope  

-   **Operating System Image**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope  

-   **Operating System Installation Package**: Create, Delete, Modify, Modify Folder, Move Object, Read, Set Security Scope  

-   **Task Sequence Package**: Create, Create Task Sequence Media, Delete, Modify, Modify Folder, Modify Report, Move Object, Read, Run Report, Set Security Scope  

 For more information, see [Create custom security roles](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### Security scopes for OS deployments  
 Use security scopes to provide administrative users with access to the securable objects used in OS deployments, such as OS and boot images, driver packages, and task sequence packages. For more information, see [Security scopes](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="BKMK_WDS"></a> Windows Deployment Services  
 Windows Deployment Services (WDS) must be installed on the same server as the distribution points that you configure to support PXE or multicast. WDS is included in the operating system of the server. For PXE deployments, WDS is the service that performs the PXE boot. When the distribution point is installed and enabled for PXE, Configuration Manager installs a provider into WDS that uses the WDS PXE boot functions.  

> [!NOTE]  
>  If the server requires a restart, the installation of WDS might fail. 


### WDS requirements  

-   The WDS installation on the server requires that the administrator is a member of the local Administrators group.  

-   The WDS server must be either a member of an Active Directory domain or a domain controller for an Active Directory domain. All Windows domain and forest configurations support WDS.  

-   If the provider is installed on a remote server, you must install WDS on the site server and the remote provider.  


###  <a name="BKMK_WDSandDHCP"></a> Considerations when you have WDS and DHCP on the same server  
 Consider the following configuration issues if you plan to co-host the distribution point on a server running DHCP.  

-   You must have a functioning DHCP server with an active scope. WDS uses PXE, which requires a DHCP server.  

-   DHCP and WDS both require port number 67. If you co-host WDS and DHCP, you can move DHCP or the distribution point that is configured for PXE to a separate server. Or, you can use the following procedure to configure the WDS server to listen on a different port.  

    #### To configure the WDS server to listen on a different port  

    1.  Modify the following registry key:  

         `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

    2.  Set the registry value **UseDHCPPorts** to **0**.  

    3.  For the new configuration to take effect, run the following command on the server:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   A DNS server is required to run WDS.  

-   The following UDP ports must be open on the WDS server.  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  If DHCP authorization is required on the server, you need DHCP client port 68 to be open on the server.  



##  <a name="BKMK_SupportedOS"></a> Supported operating systems  
 All Windows operating systems listed as supported clients in [Supported operating systems for clients and devices](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) are supported for OS deployment.  



##  <a name="BKMK_SupportedDiskConfig"></a> Supported disk configurations  
 The hard disk configuration combinations on the reference and destination computers that are supported for Configuration Manager OS deployment are shown in the following table:  

|Reference computer hard disk configuration|Destination computer hard disk configuration|  
|------------------------------------------------|--------------------------------------------------|  
|Basic disk|Basic disk|  
|Simple volume on a dynamic disk|Simple volume on a dynamic disk|  

 Configuration Manager supports capturing an OS image only from computers that are configured with simple volumes. There's no support for the following hard disk configurations:  

-   Spanned volumes  

-   Striped volumes (RAID 0)  

-   Mirrored volumes (RAID 1)  

-   Parity volumes (RAID 5)  

 The following table shows an additional hard disk configuration on the reference and destination computers that isn't supported with Configuration Manager OS deployment.  

|Reference computer hard disk Configuration|Destination computer hard disk configuration|  
|------------------------------------------------|--------------------------------------------------|  
|Basic disk|Dynamic disk|  



## Next steps
- [Prepare site system roles for OS deployments](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [Prepare for OS deployment](../get-started/prepare-for-operating-system-deployment.md)
