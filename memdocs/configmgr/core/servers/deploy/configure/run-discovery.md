---
title: Discover device and user resources
titleSuffix: Configuration Manager
description: Read an overview of the discovery process and discovery data records.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Run discovery for Configuration Manager

*Applies to: Configuration Manager (current branch)*

You use one or more discovery methods in Configuration Manager to find device and user resources that you can manage. You can also use discovery to identify network infrastructure in your environment. There are several different methods you can use to discover different things, and each method has its own configurations and limitations.  

## Overview of discovery  
 Discovery is the process by which Configuration Manager learns about the things you can manage. The following are the available discovery methods:  

-   Active Directory Forest Discovery  

-   Active Directory Group Discovery  

-   Active Directory System Discovery  

-   Active Directory User Discovery  

-   Azure Active Directory User Discovery  

-   Azure Active Directory User Group Discovery  

-   Heartbeat Discovery  

-   Network Discovery  

-   Server Discovery  

> [!TIP]  
>  You can learn about the individual discovery methods in [About discovery methods for Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  For assistance in selecting which methods to use, and at which sites in your hierarchy, see [Select discovery methods to use for Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 To use most discovery methods, you must enable the method at a site, and set it up to search specific network or Active Directory locations. When it runs, it queries the specified location for information about devices or users that Configuration Manager can manage. When a discovery method successfully finds information about a resource, it puts that information into a file called a discovery data record (DDR). That file is then processed by a primary or central administration site. Processing of a DDR creates a new record in the site database for newly discovered resources, or updates existing records with new information.  

 Some discovery methods can generate a large volume of network traffic, and the DDRs they produce can result in a significant use of CPU resources during processing. Therefore, plan to use only those discovery methods that you require to meet your goals. You might start by using  only one or two discovery methods, and then later enable additional methods in a controlled manner to extend the level of discovery in your environment.  

 After discovery information is added to the site database, the information then replicates to each site in the hierarchy, regardless of where it was discovered or processed. Therefore, while you can set up different schedules and settings for discovery methods at different sites, you might run a specific discovery method at only a single site. This reduces the use of network bandwidth through duplicate discovery actions, and reduces the  processing of redundant discovery data at multiple sites.  

 You can use discovery data to create custom collections and queries that logically group resources for management tasks. For example:  

-   Pushing client installations, or upgrading.  

-   Deploying content to users or devices.  

-   Deploying client settings and related configurations.

##  <a name="BKMK_DDRs"></a> About discovery data records  
 DDRs are files created by a discovery method. They contain information about a resource you can manage in Configuration Manager, such as computers, users, and in some cases, network infrastructure. They are processed at primary sites or at central administration sites. After the resource information in the DDR is entered into the database, the DDR is deleted, and the information replicates as global data to all sites in the hierarchy.  

 The site at which a DDR is processed depends on the information it contains:  

-   DDRs for newly discovered resources that are not in the database are processed at the top-level site of the hierarchy. The top-level site creates a new resource record in the database, and assigns it a unique identifier. DDRs transfer by file-based replication until they reach the top-level site.  

-   DDRs for previously discovered objects are processed at primary sites. Child primary sites do not transfer DDRs to the central administration site when the DDR contains information about a resource that is already in the database.  

-   Secondary sites do not process DDRs, and always transfer them by file-based replication to their parent primary site.  

DDR files are identified by the .ddr extension, and have a typical size of about 1 KB.  

## Get started with discovery:  
 Before using the Configuration Manager console to set up discovery, you should understand the differences among the methods, what they can do, and for some, their limitations.  

The following topics can build a foundation that will help you use discovery methods successfully:  

-   [About discovery methods for Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Select discovery methods to use for Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Then, when you understand the methods you want to use, find guidance to set up each method in [Configure discovery methods for Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
