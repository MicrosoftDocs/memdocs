---
title: "Supported configurations"
titleSuffix: "Configuration Manager"
description: "Identify key configurations and requirements so you can plan, deploy, and maintain a functional System Center Configuration Manager deployment."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: 9
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Supported configurations for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
As an on-premises solution, System Center Configuration Manager makes use of your servers, clients, network configurations, and additional products like Microsoft Intune, SQL Server, and Azure.

The information in this and the following topics is essential for helping you identify key configurations, requirements, and limitations, so that you can plan, deploy, and maintain a functional Configuration Manager deployment.  This information is specific to the infrastructure for Configuration Manager sites, hierarchies, and managed devices.

When a Configuration Manager feature or capability requires more specific configurations, that information is included with the feature-specific documentation, and is supplemental to the more general configuration details.  

 The products and technologies that are described in the following topics are supported by Configuration Manager. However, their inclusion in this content does not imply an extension of support for any product beyond that product's individual support lifecycle. Products that are beyond their support lifecycle are not supported for use with Configuration Manager. For more information about Microsoft Support Lifecycles, visit the [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270) website.  

> [!NOTE]  
>  For information about Microsoft support lifecycle policy, go to the Microsoft Support Lifecycle Support Policy FAQ website at [Microsoft Support Lifecycle Policy FAQ](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Additionally, products and product versions that are not listed in the following topics are not supported with System Center Configuration Manager unless they have been announced on the [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/).  At times, the content on this blog precedes an update to this body of documentation.


-  [Size and scale numbers](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Learn about how many sites, site system roles per site, and clients or devices are supported in different hierarchy designs for Configuration Manager.

-  [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Learn about configurations that are required on a Windows Server to support different site types and site system roles.

-  [Supported operating systems for site system servers](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Learn about which operating systems you can use as a site server or site system server.

-  [Supported operating systems for clients and devices](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Learn about which operating systems you can manage with Configuration Manager, including Windows, Windows Embedded, Linux and UNIX, Mac, and mobile devices.

-  [Supported operating systems for the console](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Learn about which operating systems can host the Configuration Manager console to provide a point of access for managing your deployment.  

-  [Support for SQL Server versions](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Learn about which versions of SQL Server can host the site database and reporting database, as well as about required configurations and optional configurations that you can use.

-  [High-availability options](../../../protect/understand/high-availability-options.md)  
Learn about the options you can implement when designing your environment to help maintain a high level of available service for your Configuration Manager deployment.

-  [Recommended hardware](../../../core/plan-design/configs/recommended-hardware.md)  
Learn about guidelines that can help you identify the right hardware and configurations to host your Configuration Manager sites and key services.

-  [Support for Active Directory domains](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Learn about the supported Active Directory domain configurations that Configuration Manager requires and supports.

-  [Support for Windows features and networks](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Learn about supported Windows technologies  (such as BranchCache and data deduplication) and limitations for their use with Configuration Manager.

-  [Support for virtualization environments](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Learn more about how to use supported virtual machine technologies.
