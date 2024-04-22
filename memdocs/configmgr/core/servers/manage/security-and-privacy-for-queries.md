---
title: Security and privacy for queries
titleSuffix: Configuration Manager
description: Understand best practices for security and privacy when you query for information from the site database.
ms.date: 05/08/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Security and privacy for queries in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Queries in Configuration Manager let you retrieve information from the site database according to criteria that you specify. Configuration Manager collects site database information during standard operation. For example, by using information that's been collected during discovery or inventory, you can configure a query to identify devices that meet specified criteria.  

 For more information about queries, see [Introduction to queries](../../../core/servers/manage/introduction-to-queries.md). For security best practices and privacy information about Configuration Manager operations that collect the data you can retrieve by using queries, see [Security and privacy for Configuration Manager](../../../security/index.yml).  

## Security best practices for queries

 Use this security best practice for queries.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|When you export or import a query that's saved to a network location, secure the location and the network channel.|Restrict who can access the network folder.<br /><br /> Use Server Message Block (SMB) signing or Internet Protocol security (IPsec) between the network location and the site server to prevent an attacker from tampering with the query data before it's imported.|  

## Next steps
  
[Security and privacy for Configuration Manager](../../../security/index.yml)