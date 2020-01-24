---
title: Choose a device management solution
titleSuffix: Configuration Manager
description: Learn about the solutions that Configuration Manager offers for managing PCs, servers, and devices.
ms.date: 07/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Choose a device management solution for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager offers different solutions for managing PCs, servers, and devices. Choose the solution that's right for your organization. Base your decision on the device platforms you need to manage and the management functionality you need.  

## Overview

This article primarily covers the following four device management solutions:

- [Configuration Manager client](#bkmk_sccm)
- [On-premises mobile device management (MDM) with Configuration Manager](#bkmk_opmdm)
- [Co-management with Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

You can use these solutions by themselves or in combination with each other. For example, use the client-based management approach to manage the computers and servers in your organization, and also use co-management to manage internet-based laptops. By combining approaches this way, you can cover all of your device management needs.  

The article also includes two tables that compare the management solutions by the following factors:

- [Compare by supported platforms](#bkmk_comp1)
- [Compare by management functionality](#bkmk_comp2)

### <a name="bkmk_sccm"></a> Configuration Manager client  

This option requires installation of the Configuration Manager client on devices. It provides the most features for managing PCs, servers, and other devices in your environment.

For more information, see [Client installation methods](/sccm/core/clients/deploy/plan/client-installation-methods).  

### <a name="bkmk_opmdm"></a> On-premises MDM  

This option uses the device management capabilities built into Windows 10. While not as full-featured as client-based management, on-premises MDM provides a lighter touch approach to management. It uses on-premises Configuration Manager resources to manage devices.  

For more information, see [Manage mobile devices with on-premises infrastructure](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

### <a name="bkmk_comanage"></a> Co-management with Microsoft Intune

Co-management is one of the primary ways to attach your existing Configuration Manager deployment to the Microsoft 365 cloud. It enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. Co-management lets you cloud-attach your existing investment in Configuration Manager by adding new functionality.

For more information, see [What is co-management?](/sccm/comanage/overview).  

### <a name="bkmk_exchange"></a> Microsoft Exchange  

This option uses the Exchange Server connector to connect multiple Exchange servers to Configuration Manager. It centralizes management of devices that can connect to Exchange ActiveSync. You can configure Exchange mobile device management features from the Configuration Manager console. Example features include remote device wipe and the settings control for multiple Exchange servers.

For more information, see [Manage mobile devices with Configuration Manager and Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


## <a name="bkmk_comp1"></a> Compare solutions by supported platforms  

|Platform|Configuration Manager client|On-premises MDM|Configuration Manager with Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Yes| Yes |
|iOS| | |Yes| Yes |
|Mac OS X|Yes| |Yes| Yes |
|Windows 10|Yes|Yes|Yes| Yes |
|Windows 10 Mobile| |Yes|Yes| Yes |
|Windows (previous versions)|Yes| |Yes|  |
|Windows Server|Yes| |Yes|  |
|Windows Embedded|Yes| | |  |

For a complete list of supported platforms, see the following articles:

- [Supported operating systems for clients and devices for Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)
- [Intune supported configurations](https://docs.microsoft.com/intune/supported-devices-browsers)

Microsoft recommends using Intune to manage Android, iOS, and Windows 10 mobile devices. For more information, see [What is Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune).


## <a name="bkmk_comp2"></a> Compare solutions by management functionality  

|Management functionality|Configuration Manager client|On-premises MDM|Configuration Manager with Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Public key infrastructure (PKI) security between the mobile device and Configuration Manager (uses mutual authentication and SSL to encrypt data transfers)|Yes|Yes| |  
|Client installation|Yes| | |  
|Support over the internet|Yes| | |  
|Discovery|Yes| |Yes|  
|Hardware inventory|Yes|Yes|Yes|  
|Software inventory|Yes| |Yes|  
|Settings|Yes|Yes|Yes|  
|Software deployment|Yes|Yes| |  
|Monitor with fallback status point|Yes| | |  
|Connections to management points|Yes|Yes| |  
|Connections to distribution points|Yes|Yes| |  
|Block from Configuration Manager|Yes|Yes| |  
|Quarantine and block from Exchange Server (and Configuration Manager)| | |Yes|  
|Remote wipe| |Yes|Yes|  


## <a name="bkmk_other"></a> Other Microsoft solutions

There are other Microsoft solutions that might work better for you in different scenarios. Use the following table to help compare these additional management technologies:

|  | Cloud-only | Cloud-attached | On-premises | Disconnected |
|---------|---------|---------|---------|---------|
| **Hyper-V host** | Not applicable | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager |
| **Windows Server** | - Azure management<br/> - Configuration Manager | - Azure management<br/> - Configuration Manager | - Azure management<br/> - Configuration Manager | Configuration Manager |
| **Linux Server** | Azure management | Azure management | Azure management |  |
| **Windows 10** | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | Configuration Manager |
| **Windows 7 or 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Virtual Desktop** | Configuration Manager | Not applicable | Not applicable | Not applicable |

For more information on these technologies, see the following articles:

- [What is Azure Stack?](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [What is Windows Admin Center?](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [What is Virtual Machine Manager?](https://docs.microsoft.com/system-center/vmm/overview)
- [Azure management products](https://docs.microsoft.com/azure/#pivot=products&panel=mgmt)
- [Configuration Manager on Azure](/sccm/core/understand/configuration-manager-on-azure)
- [What is Windows Virtual Desktop?](https://docs.microsoft.com/azure/virtual-desktop/overview)
