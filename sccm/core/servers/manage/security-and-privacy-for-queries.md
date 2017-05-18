---
title: "Security and privacy for queries | Microsoft Docs"
description: "Understand best practices for security and privacy when you query for information from the site database."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsftms.author: robstackmanager: angrobe

---
# Security and privacy for queries in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Queries in System Center Configuration Manager let you retrieve information from the site database based on the criteria that you specify. Configuration Manager collects the site database information during standard operation. For example, by using information that has been collected from discovery or inventory, you can configure a query to identify devices that meet specified criteria.  

 For more information about queries, see [Introduction to queries in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). For more information about security best practices and privacy information for Configuration Manager operations that collect the information that you can retrieve by using queries, see [Security and privacy for System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## Security Best Practices for Queries  
 Use the following security best practice for queries.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|When you export or import a query that is saved to a network location, secure the location and the network channel.|Restrict who can access the network folder.<br /><br /> Use server message block (SMB) signing or Internet Protocol Security (IPsec) between the network location and the site server to prevent an attacker from tampering with the query data before it is imported.|  

## See also  
 [Queries technical reference for System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
