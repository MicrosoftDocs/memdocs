---
title: "Diagnostics and usage data for System Center Configuration Manager"
ms.custom: na
ms.date: 2016-03-11
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
author: Brenduns
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Diagnostics and usage data for System Center Configuration Manager
System Center Configuration Manager collects diagnostics and usage data about itself which is used by Microsoft to improve the installation experience, quality, and security of future releases.  
  
 Diagnostics  and Usage Data is enabled for each System Center Configuration Manager hierarchy. It consists of SQL Server queries that run on a weekly basis on each primary site and at central administration site. When the hierarchy uses a central administration site, the data from primary sites is then replicated to that site. At the top-level site of your hierarchy, the service connection point submits this information when it checks for updates. If the service connection point is in offline mode, the information is transferred by using the service connection tool.  
  
> [!NOTE]  
>  Configuration Manager only collects data from the sites SQL server database, and does not collect data directly from clients or site servers.  
  
 For more information see the [Privacy Statement for System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  
  
 Learn more about diagnostic and usage data for System Center Configuration Manager in the following topics:  
  
-   [How diagnostics and usage data is used for System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  
  
-   [Levels of diagnostic usage data collection for System Center Configuration Manager](../../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection.md)  
  
-   [How diagnostics and usage data is collected by System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  
  
-   [How to view diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  
  
-   [Customer Experience Improvement Program (CEIP) for System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  
  
-   [Frequently asked questions about diagnostics and usage data for System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  
  
## See Also  
 [Technical reference for System Center Configuration Manager](../Topic/Technical%20reference%20for%20System%20Center%20Configuration%20Manager.md)   
 [Site installation technical reference for System Center Configuration Manager](../Topic/Site%20installation%20technical%20reference%20for%20System%20Center%20Configuration%20Manager.md)   
 [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)