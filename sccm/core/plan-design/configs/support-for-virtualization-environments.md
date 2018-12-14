---
title: "Support for virtualization"
titleSuffix: "Configuration Manager"
description: "Get requirements for installing System Center Configuration Manager client and site system roles in a virtualization environment."
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Support for virtualization environments for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager supports installing the client and site system roles on supported operating systems that run as a virtual machines in the virtualization environments that are listed in this article. This support exists even when the virtual machine host (virtualization environment) is not supported as a client or site server.  

 For example, if you use Microsoft Hyper-V Server 2012 to host a virtual machine that runs Windows Server 2012, you can install the client or site system roles on the virtual machine (Windows Server 2012), but not on the host (Microsoft Hyper-V Server 2012).  


|            Virtualization environment             |
|---------------------------------------------------|
|              Windows Server 2008 R2               |
|         Microsoft Hyper-V Server 2008 R2          |
|                Windows Server 2012                |
|           Microsoft Hyper-V Server 2012           |
|              Windows Server 2012 R2               |
|   Windows Server 2016 <sup>(See *note 1*)</sup>   |
| Microsoft Hyper-V Server 2016 <sup>(See *note 1*) |

-  *Note 1*: Configuration Manager does not support [nested virtualization](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), which is new with Windows Server 2016.


 Each virtual computer that you use must meet or exceed the same hardware and software requirements that you would use for a physical Configuration Manager computer.  

 You can validate that your virtualization environment is supported for Configuration Manager by using the Server Virtualization Validation Program and its online Virtualization Program Support Policy Wizard. For more information about the Server Virtualization Validation Program, see [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  Configuration Manager does not support Virtual PC or Virtual Server guest operating systems that run on Mac computers.  

Configuration Manager cannot manage virtual machines unless they are online. An offline virtual machine image cannot be updated nor can inventory be collected by using the Configuration Manager client on the host computer.  

No special consideration is given to virtual machines. For example, Configuration Manager might not determine whether an update has to be re-applied to a virtual machine image if the virtual machine has been stopped and restarted without saving the state of the virtual machine to which the update was applied.  

##  <a name="bkmk_Azure"></a> Microsoft Azure virtual machines  
 Configuration Manager can run on virtual machines in Azure just as it runs on-premises within your physical corporate network. You can use Configuration Manager with Azure virtual machines in the following scenarios:  

-   **Scenario 1:** You can run Configuration Manager on an Azure virtual machine and use it to manage clients that are installed on other Azure virtual machines.  

-   **Scenario 2:** You can run Configuration Manager on an Azure virtual machine and use it to manage clients that are not running on Azure.  

-   **Scenario 3:** You can run different Configuration Manager site system roles on Azure virtual machines while running other roles in your physical corporate network (with appropriate network connectivity for communications).  

The same System Center Configuration Manager requirements for networks, supported configurations, and hardware requirements that apply to installing Configuration Manager on-premises on your physical corporate network also apply to installation on Azure virtual machines.  

For more information, see [Configuration Manager on Azure--Frequently Asked Questions](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  Configuration Manager sites and clients that run on Azure virtual machines are subject to the same license requirements as on-premises installations.  
