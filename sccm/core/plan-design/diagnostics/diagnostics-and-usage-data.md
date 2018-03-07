---
title: Diagnostics and usage data
titleSuffix: Configuration Manager
description: Learn about the diagnostics and usage data that System Center Configuration Manager collects about itself.
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Diagnostics and usage data for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager collects diagnostics and usage data about itself, which is used by Microsoft to improve the installation experience, quality, and security of future releases.  

 Diagnostics and usage data is enabled for each Configuration Manager hierarchy. It consists of SQL Server queries that run on a weekly basis on each primary site and at the central administration site. When the hierarchy uses a central administration site, the data from primary sites is then replicated to that site. At the top-level site of your hierarchy, the service connection point submits this information when it checks for updates. If the service connection point is in offline mode, the information is transferred by using the service connection tool.  

> [!NOTE]  
>  Configuration Manager collects data only from the site's SQL server database, and it does not collect data directly from clients or site servers.  

 For more information, see the [Microsoft privacy statement](https://go.microsoft.com/fwlink/?LinkID=626527).  

## Articles
 Learn more about diagnostic and usage data for Configuration Manager in the following articles:  

-   [How diagnostics and usage data is used](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Levels of diagnostic usage data collection:
    - [Diagnostic data for 1802](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    - [Diagnostic data for 1710](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  
    - [Diagnostic data for 1706](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1706)    

<!--
    - [Diagnostic data for 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Diagnostic data for 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Diagnostic data for  1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [How diagnostics and usage data is collected](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [How to view diagnostics and usage data](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Customer Experience Improvement Program (CEIP)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

     > [!Note]  
     > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.


-   [Frequently asked questions about diagnostics and usage data](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## See Also  
 [About the service connection point](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
