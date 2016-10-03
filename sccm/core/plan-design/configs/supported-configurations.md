---
title: "Supported configurations | System Center Configuration Manager"
description: "Identify key configurations and requirements so you can plan, deploy, and maintain a functional System Center Configuration Manager deployment."
ms.custom: na
ms.date: 07/22/2016
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
# Supported configurations for System Center Configuration Manager
As an on-premises solution, System Center Configuration Manager makes use of your servers, clients, network configurations, and additional products like Microsoft Intune, SQL Server and Azure.

The information in this and the following topics is essential to identifying key configurations and requirements, or limitations, so you can plan, deploy, and maintain a functional Configuration Manager deployment.  This information is specific to the infrastructure for Configuration Manager sites, hierarchies and managed devices. When a Configuration Manager feature or capability requires more specific configurations, that information will be included with the feature specific documentation, and is supplemental to these more general supported configuration details.  

 The products and technologies detailed in the following topics are supported with Configuration Manager. However, their inclusion in this content does not express an extension of support for any product beyond that products individual support lifecycle. Products that are beyond their support lifecycle are not supported for use with Configuration Manager. For more information about Microsoft Support Lifecycles, visit the [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270) website.  

> [!NOTE]  
>  For information about Microsoft support lifecycle policy, go to the Microsoft Support Lifecycle Support Policy FAQ website at [Microsoft Support Lifecycle Policy FAQ](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Additionally, products and product versions that are not listed in the following topics are not supported with System Center Configuration Manager unless they have been announced on the [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/).  At times, the content on this blog will precede an update to this body of documentation.


-  [Size and scale numbers](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Details about how many sites, site system roles per site, and clients or devices are supported in different hierarchy designs for Configuration Manager.

-  [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Configurations that are required on a Windows server to support different site types and site system roles.

-  [Supported operating systems for site system servers](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Learn which operating systems you can use as a site server or site system server.

-  [Supported operating systems for clients and devices](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Learn which operating systems you can manage with Configuration Manager, including Windows, Linux and UNIX, Mac, Embedded operating systems, and mobile devices.

-  [Supported operating systems for the console](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Learn which operating systems can host the Configuration Manager console to provide a point of access for managing your deployment.  

-  [Support for SQL Server versions](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Lists the versions of SQL Server that can host the site database and reporting database, as well as required configurations and optional configurations you can choose to use.

-  [High availability options](../../../protect/understand/high-availability-options.md)  
Learn about the options you can implement when designing your environment to help maintain a high level of available service for your Configuration Manager deployment.

-  [Recommended hardware](../../../core/plan-design/configs/recommended-hardware.md)  
Guidelines that can help you identify the right hardware and configurations to host your Configuration Manager sites and key services.

-  [Support for Active Directory domains](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Learn about the supported Active Directory domain configurations Configuration Manager requires, and supports.

-  [Support for Widows features and networks](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Configuration Manager supports several Windows technologies like BranchCache and data deduplication. Learn about supported technologies and limitations for their use with Configuration Manager.

-  [Support for Virtualization environments](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Information to help you use supported virtual machine technologies.
