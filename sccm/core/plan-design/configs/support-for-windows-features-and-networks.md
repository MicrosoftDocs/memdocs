---
title: Support for Windows features
titleSuffix: Configuration Manager
description: Learn which Windows and networking features Configuration Manager supports.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Support for Windows features and networks in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article identifies Configuration Manager support for common Windows and networking features.  



##  <a name="bkmk_branchcache"></a> BranchCache  

Use Windows BranchCache with Configuration Manager when you enable it on distribution points, and configure clients to use it in distributed cache mode.

Configure the BranchCache settings on a deployment type for applications, on the deployment for a package, and for task sequences. Starting in version 1802, BranchCache is enabled by default. 

When the requirements for BranchCache are met, this feature enables clients in remote locations to obtain content from local clients that have a current cache of the content.  

For example, when the first BranchCache-enabled client requests content from a distribution point that's configured as a BranchCache server, the client downloads and caches the content. This content is then made available for clients on the same subnet that requested this content.

These clients also cache the content. Other clients on the same subnet don't have to download content from the distribution point. The content is distributed across multiple clients for future transfers.  


### Requirements to support BranchCache with Configuration Manager

#### Configure distribution points
Add the **Windows BranchCache** feature to the site system server that's configured as a distribution point.    
- Distribution points on servers that are configured to support BranchCache require no additional configuration.   
- You can't add Windows BranchCache to a cloud-based distribution point. Cloud-based distribution points do support the download of content by clients that are configured for Windows BranchCache.  

#### Configure clients    
- The clients that can support BranchCache must be configured for BranchCache distributed cache mode.  
- The OS setting for BITS client settings must be enabled to support BranchCache.  

For information, see [configure clients for BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) in the Windows documentation.


### Configuration Manager supported OS versions with Windows BranchCache

|Operating system|Support details|  
|----------------------|---------------------|  
|Windows 7 with SP1|Supported by default|  
|Windows 8|Supported by default|  
|Windows 8.1|Supported by default|  
|Windows 10|Supported by default|  
|Windows Server 2008 with SP2|**Requires BITS 4.0**: Install the BITS 4.0 release on Configuration Manager clients by using software updates or software distribution. For more information, see [Windows Management Framework](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits).<br /><br /> On this OS, the BranchCache client functionality isn't supported for software distribution that's run from the network or for SMB file transfers. Additionally, this OS can't use BranchCache functionality with cloud-based distribution points.|  
|Windows Server 2008 R2|Supported by default|  
|Windows Server 2012|Supported by default|  
|Windows Server 2012 R2|Supported by default|  
|Windows Server 2016|Supported by default|  

For more information, see [BranchCache for Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) in the Windows Server documentation.  



##  <a name="bkmk_Workgroups"></a> Computers in workgroups  

Configuration Manager provides support for clients in workgroups.  

- Configuration Manager supports moving a client from a workgroup to a domain or from a domain to a workgroup. For more information, see [How to install Configuration Manager clients on workgroup computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup).  

> [!NOTE]  
>  Although clients in workgroups are supported, all site systems must be members of a supported Active Directory domain.  



##  <a name="bkmmk_datadedup"></a> Data deduplication  

Configuration Manager supports the use of data deduplication with distribution points on the following operating systems:  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  The volume that hosts package source files can't be marked for data deduplication. This limitation is because data deduplication uses reparse points. Configuration Manager doesn't support using a content source location with files stored on reparse points.  

For more information, see [Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/) on the Configuration Manager team blog, and [Data Deduplication Overview](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) in the Windows Server documentation.  



##  <a name="bkmk_DA"></a> DirectAccess  

Configuration Manager supports the DirectAccess feature for communication between clients and site server systems.  

- When all the requirements for DirectAccess are met, it enables Configuration Manager clients on the internet to communicate with their assigned site as if they were on the intranet.  

- For server-initiated actions, such as remote control and client push installation, the initiating computer must be running IPv6. This protocol must be supported on all intervening networking devices.  

Configuration Manager doesn't support the following functionality over DirectAccess:  

-   OS deployment   

-   Communication between Configuration Manager sites  

-   Communication between Configuration Manager site system servers within a site  



##  <a name="bkmk_dualboot"></a> Dual boot computers  

Configuration Manager can't manage more than one OS on a single computer. If there's more than one OS on a computer to manage, adjust the site's discovery and client installation methods to ensure that the Configuration Manager client is installed only on the OS that has to be managed.  



##  <a name="bkmk_IPv6"></a> Internet Protocol version 6  

In addition to Internet Protocol version 4 (IPv4), Configuration Manager supports Internet Protocol version 6 (IPv6) with the following exceptions:  

|Function| Exception to IPv6 support|  
|--------------|-------------------------------|  
|Cloud-based distribution points|IPv4 is required to support Microsoft Azure and cloud-based distribution points.|  
|Cloud management gateway|IPv4 is required to support Microsoft Azure and the cloud management gateway.|  
|Mobile devices that are enrolled by Microsoft Intune and the Microsoft service connector|IPv4 is required to support mobile devices that are enrolled by Microsoft Intune and the Microsoft service connector.|  
|Network Discovery|IPv4 is required when you configure a DHCP server to search in Network Discovery.|  
|OS deployment|In version 1802 and prior, IPv4 is required to support OS deployment. </br></br>Starting in version 1806, enable a PXE responder on a distribution point without Windows Deployment Service. This new PXE responder service supports IPv6. Other aspects of the OS deployment feature, such as capturing or setting static IP addresses during the task sequence, continue to require IPv4. |  
|Wake-up proxy communication|IPv4 is required to support the client wake-up proxy packets.|  
|Windows CE|IPv4 is required to support the Configuration Manager client on Windows CE devices.|  



##  <a name="bkmk_NAT"></a> Network Address Translation  

Network Address Translation (NAT) isn't supported in Configuration Manager, unless the site supports clients that are on the internet and the client detects that it's connected to the internet. For more information about internet-based client management, see [Plan for managing internet-based clients](/sccm/core/clients/deploy/plan/plan-for-managing-internet-based-clients).  



##  <a name="bkmk_storage"></a> Specialized storage technology  

Configuration Manager works with any hardware that's certified on the Windows Hardware Compatibility List for the version of the OS that the Configuration Manager component is installed on.

Site server roles require NTFS, so that Configuration Manager can set directory and file permissions. Configuration Manager assumes that it has complete ownership of a logical drive. Site systems that run on separate computers can't share a logical partition on any storage technology. However, each computer can use a separate logical partition on the same physical partition of a shared storage device.  

### Support considerations

- **Storage Area Network**: A Storage Area Network (SAN) is supported when a supported Windows-based server is attached directly to the volume that's hosted by the SAN.  

- **Single Instance Storage**: Configuration Manager doesn't support configuration of distribution point package and signature folders on a Single Instance Storage (SIS)-enabled volume.  

     Additionally, the cache of a Configuration Manager client isn't supported on a SIS-enabled volume.  

- **Removable disk drive**: Configuration Manager doesn't support the installation of Configuration Manager site systems or clients on a removable disk drive.  
