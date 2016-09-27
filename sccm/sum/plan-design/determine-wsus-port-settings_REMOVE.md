---
title: "How to determine the port settings used by WSUS in System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-sum
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb5a042f-5c66-424e-8b42-810d971e95ff
caps.latest.revision: 6
author: Dougeby

---
# How to determine the port settings used by WSUS in System Center Configuration Manager
When you install and configure a software update point in System Center Configuration Manager, the port settings used by the Microsoft Windows Server Update Services (WSUS) server must be specified.  Use the following procedure to determine the port settings used by WSUS.  
  
### To determine the port settings used in IIS  
  
1.  On the WSUS server, open Internet Information Services (IIS) Manager.  
  
2.  Expand **Sites**, right-click the Web site for the WSUS server, and then click **Edit Bindings**. In the Site Bindings dialog, the HTTP and HTTPS port values are displayed in the **Port** column.  
  
## See Also  
 [Configure software updates in System Center Configuration Manager](../../sum/deploy-use/configure-software-updates.md)

