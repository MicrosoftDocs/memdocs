---
title: Support for virtualization
titleSuffix: Configuration Manager
description: The requirements for installing Configuration Manager client and site system roles in a virtualization environment.
ms.date: 01/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Support for virtualization environments with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager supports installing the client and site system roles on supported operating systems that run as a virtual machine in the virtualization environments in this article. This support exists even when the virtual machine host (virtualization environment) isn't supported as a client or site server.  

For example, you use Microsoft Hyper-V Server 2012 to host a virtual machine that runs Windows Server 2012. You can install the client or site system roles on the virtual machine running Windows Server 2012. You can't install the client on the host running Microsoft Hyper-V Server 2012.  


## Virtualization environments

- Windows Server 2019  
- Windows Server 2016 <sup>[Note 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Note 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  
- Microsoft Hyper-V Server 2008 R2  
- Windows Server 2008 R2  

#### <a name="bkmk_note1"></a> Note 1: Nested virtualization
Configuration Manager doesn't support [nested virtualization](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#BKMK_nested), which is new with Windows Server 2016.


### Virtualization environment support

Each virtual computer needs the same or greater hardware and software requirements that you would use for a physical Configuration Manager computer.  

To validate that your virtualization environment is supported for Configuration Manager, use the Server Virtualization Validation Program. It includes an online Virtualization Program Support Policy Wizard. For more information, see [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> Configuration Manager doesn't support Virtual PC or Virtual Server guest operating systems that run on Mac computers.  

Configuration Manager can't manage virtual machines if they're offline. An offline virtual machine image can't be updated nor can inventory be collected by using the Configuration Manager client on the host computer.  

No special consideration is given to virtual machines. For example, Configuration Manager might not determine whether an update has to be reapplied to a virtual machine image if the virtual machine has been stopped and restarted without saving the state of the virtual machine to which the update was applied.  



##  <a name="bkmk_Azure"></a> Microsoft Azure virtual machines  

Configuration Manager can run on virtual machines in Azure just as it runs on-premises within your data center. Use Configuration Manager with Azure virtual machines in the following scenarios:  

- **Scenario 1**: Run Configuration Manager on an Azure virtual machine. Use it to manage clients on other Azure virtual machines.  

- **Scenario 2**: Run Configuration Manager on an Azure virtual machine. Use it to manage clients that aren't running on Azure.  

- **Scenario 3**: Run different Configuration Manager site system roles on Azure virtual machines. Run other roles in your on-premises data center, properly connected to Azure.  

The same Configuration Manager requirements for networks, supported configurations, and hardware requirements that apply to installing it on-premises also apply to installation on Azure virtual machines.  

For more information, see [Configuration Manager on Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
> Configuration Manager sites and clients that run on Azure virtual machines are subject to the same license requirements as on-premises installations.  
