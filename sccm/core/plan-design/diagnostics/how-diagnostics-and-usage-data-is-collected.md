---
title: "How diagnostics and usage data is collected by System Center Configuration Manager"
ms.custom: na
ms.date: 2016-03-11
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: 5
author: Brenduns
translation.priority.ht: 
  - cs-cz
  - de-de
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
# How diagnostics and usage data is collected by System Center Configuration Manager
To collect diagnostics and usage data for System Center Configuration Manager, each primary site runs SQL Server queries on a weekly basis. In a multi-site hierarchy, the data is replicated to the central administration site.  
  
 At the top-level site of a hierarchy, the service connection point site system role submits this information when it checks for updates. How the data transfers depends on the mode of the service connection point:  
  
-   **In online mode:** Diagnostics and usage data is automatically sent once a week from the service connection point to the cloud service.  
  
-   **In offline mode:** Diagnostics and usage data is transferred manually by using the service connection tool. For more information, see [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  
  
 For more information, see [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
  
## See Also  
 [Diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)   
 [Levels of diagnostic usage data collection for System Center Configuration Manager](../../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection.md)   
 [How diagnostics and usage data is used for System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)   
 [How to view diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)