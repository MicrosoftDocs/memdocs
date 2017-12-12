---
title: "Use cloud services to supplement on-premises infrastructure"
titleSuffix: "Configuration Manager"
description: "Provision cloud resources for System Center Configuration Manager to supplement your on-premises infrastructure."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: 10
caps.handback.revision: 0
author: aaronczms.author: aaroncz
manager: angrobe

---
# Use cloud services with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
System Center Configuration Manager supports several cloud-based options. These can supplement your on-premises infrastructure, and can help solve business problems like:  

-   How to manage BYOD (by using Intune for mobile device management).  

-   How to provide content resources to isolated clients or resources on the intranet, outside your corporate firewall (by using cloud-based distribution points).  

-   How to scale out infrastructure when physical hardware isn't available, or isn't logically placed to support your needs (by using Microsoft Azure virtual machines).  

Although provisioning cloud resources is not something you must do before you deploy Configuration Manager, it can be beneficial to understand these options before progressing too far in a hierarchy design plan. The use of cloud resources might save you money and time, while solving business problems that on-premises infrastructure can't.  

## Cloud-based resources you can use with Configuration Manager  
 Because each option has different requirements, investigate each in greater depth to understand the unique prerequisites, limitations, and potential for additional costs based on use.  

-   For information about cloud-based distribution points, see [Install cloud-based distribution points](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   For more information about Azure, see [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) in the MSDN Library.  

### Azure virtual machines (for cloud-based infrastructure)  
 Configuration Manager supports using computers that run in virtual machines in Azure, just as it does when run on-premises within your physical corporate network. You can use Azure virtual machines in the following scenarios:  

-   **Scenario 1:** You can run Configuration Manager in a virtual machine and use it to manage clients installed in other virtual machines.  

-   **Scenario 2:** You can run Configuration Manager in a virtual machine and use it to manage clients that are not running in Azure.  

-   **Scenario 3:** You can run different Configuration Manager site system roles in virtual machines, while running other roles in your physical corporate network (with appropriate network connectivity for communications).  

The same requirements for networks, operating systems, and hardware requirements that apply to installing the Configuration Manager on your physical corporate network also apply to the installation of Configuration Manager in Azure.  

An Azure subscription is required to use Azure virtual machines. You incur charges based on the number of virtual machines you use, their configuration, and use of cloud-based resources.  

Additionally, Configuration Manager sites and clients that run in Azure virtual machines are subject to the same license requirements as on-premises installations.  

### Azure services (for cloud-based distribution points)  
 You can use an Azure service to host a Configuration Manager distribution point, which is called a called cloud-based distribution point. You can [use a cloud-based distribution point with System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) alongside on-premises distribution points, and distribution points deployed in Azure virtual machines.  

 This is different than using an Azure virtual machine, on which you deploy a site system role. Cloud-based distribution points:  

-   Run as a service in Azure, not on a virtual machine.  

-   Automatically scale to meet increased content requests from clients.  

-   Support clients on the Internet and the intranet.  

An Azure subscription is required to use Azure to host distribution points. You incur charges based on the amount of data that transfers to and from the service.  

### Microsoft Intune (for mobile device management)  
 You can integrate your Microsoft Intune subscription with Configuration Manager to enable management of devices by using the Intune service. This integration:  

-   Is called a hybrid configuration, and it extends Configuration Manager (or Intune, depending on your perspective) to support a wide variety of devices.  

-   Requires the Microsoft Intune Connector site system role.  

-   Requires you to have a separate Intune subscription with sufficient licenses for the devices you will manage with Intune.  

Although Intune uses Azure, it does not require you to independently configure Azure, nor are you subject to additional costs beyond that of the Intune subscription.  

### Additional Configuration Manager capabilities  
 Some Configuration Manager capabilities can connect to cloud-based services, like:  

-   Windows Server Update Services (WSUS).  

-   The Configuration Manager service cloud, to download updates for Configuration Manager.  

These additional capabilities do not require you to have an Azure subscription. You don't have to set up specific connections, certificates, or services in the cloud. Instead, they are automatically managed by Configuration Manager for you. All you need to do is ensure applicable site systems and devices can access the Internet-based URLs.  

##  <a name="BKMK_CloudSec"></a> Security for cloud-based services  
 Configuration Manager uses certificates to provision and access your content in Azure, and to manage the services that you use. Configuration Manager encrypts the data that you store in Azure, but does not introduce additional security or data controls beyond those that Azure provides.  

 For more information, see the details for the different cloud-based resource scenarios. You can also view the following topics for Azure security:  

-   [Azure: Understanding Security Account Management in Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Azure Security Overview](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Get Past the Security Crossroads in Your Cloud Migration](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Data Security in Azure Part 1 of 2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  
