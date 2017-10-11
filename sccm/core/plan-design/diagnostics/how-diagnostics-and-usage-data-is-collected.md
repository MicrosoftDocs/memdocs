---
title: "Diagnostics data collection"
titleSuffix: "Configuration Manager"
description: "Learn about how System Center Configuration Manager collects diagnostics and usage data about itself."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: 5
author: Brendunsms.author: brendunsmanager: angrobe

---
# How diagnostics and usage data is collected by System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
To collect diagnostics and usage data for System Center Configuration Manager, each primary site runs SQL Server queries on a weekly basis. In a multi-site hierarchy, the data is replicated to the central administration site.  

At the top-level site of a hierarchy, the service connection point site system role submits this information when it checks for updates. The mode of the service connection point detemines how the data is transferred:  

-   **In online mode:** Diagnostics and usage data is automatically sent once a week from the service connection point to the cloud service.  

-   **In offline mode:** Diagnostics and usage data is transferred manually by using the service connection tool. For more information, see [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

For more information, see [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
