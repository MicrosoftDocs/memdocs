---
title: "Run discovery | System Center Configuration Manager"
ms.custom: na
ms.date: 04/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: 20
caps.handback.revision: 0
author: Brenduns

---
# Run discovery for System Center Configuration Manager
You use one or more discovery methods in    
      System Center Configuration Manager to find device and user resources that you can manage. You can also use Discovery to identify  network infrastructure in your environment.  There are several different Discovery methods you can use to discover different things, and each method has its own configurations and limitations.  

## Overview of discovery  
 Discovery is the process by which Configuration Manager learns about the things you can manage. The following are the available discovery methods:  

-   Active Directory Forest Discovery  

-   Active Directory Group Discovery  

-   Active Directory System Discovery  

-   Active Directory User Discovery  

-   Heartbeat Discovery  

-   Network Discovery  

-   Server Discovery  

> [!TIP]  
>  You can learn about the individual discovery methods in [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  For assistance in selecting which methods to use, and at which sites in your hierarchy, see  [Select discovery methods to use for System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 To use most discovery methods, you must enable the method at a site and configure it to search specific network or Active Directory locations. When it runs, it queries the specified location for information about devices or users that Configuration Manager can manage.  When a discovery method successfully finds information about a resource, it puts that information  into a file that is called a discovery data record (DDR), which is processed by a primary or central administration site. Processing of a DDR creates a new record in the site database for newly discovered resources, or updates existing records with new information.  

 Some discovery methods can generate a large volume of network traffic, and the resultant DDRs can result in a significant use of CPU resources during processing. Therefore,  plan to  use only those discovery methods that you require to meet your goals. You might start by using  only one or two discovery methods, and then later enable additional methods in a controlled manner to extend the level of discovery in your environment.  

 After discovery information is added to the site database it then replicates to each site in the hierarchy, regardless of at which site it was discovered or processed. Therefore, while you can configure different schedules and settings for discovery methods at different sites, you might run a specific discovery method at only a single site to   reduce the use of network bandwidth through duplicate discovery actions, and reduce the  processing of redundant discovery data at multiple sites.  

 You can use discovery data to create custom collections and queries  that logically group resources for management tasks like:  

-   Push client installations, or upgrade  

-   Deploy content to users or devices  

-   Deploy client settings and related configurations  

##  <a name="BKMK_DDRs"></a> About discovery data records  
 Discovery data records (DDRs) are files created by a discovery method and contain information about a resource you can manage in Configuration Manager. DDRs contain information about computers, users and in some cases, network infrastructure. They are processed at primary sites or at central administration sites. After the resource information in the DDR is entered into the database, the DDR is deleted and the information replicates as global data to all sites in the hierarchy.  

 The site at which a DDR is processed depends on the information it contains:  

-   DDRs for newly discovered resources that are not in the database are processed at the top-level site of the hierarchy. The top-level site creates a new resource record in the database and assigns it a unique identifier. DDRs transfer by file-based replication until they reach the top-level site.  

-   DDRs for previously discovered objects are processed at primary sites. Child primary sites do not transfer DDRs to the central administration site when the DDR contains information about a resource that is already in the database.  

-   Secondary sites do not process discovery data records and always transfer them by file-based replication to their parent primary site.  

DDR files are identified by the .ddr extension, and have a typical size of about 1 KB.  

## Get started with discovery:  
 Before using the Configuration Manager console to configure discovery you should understand the differences between the methods, what they can do, and for some, their limitations.  
The following subjects can build a foundation that will help you use Discovery methods successfully:  

-   [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Select discovery methods to use for System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Then, when you understand the methods you want to use, find guidance to configure each method in [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
