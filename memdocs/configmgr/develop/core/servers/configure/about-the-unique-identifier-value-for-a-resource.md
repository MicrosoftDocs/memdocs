---
title: Unique Identifier Value for a Resource
titleSuffix: Configuration Manager
description: An optional property that reports inventory data for a resource.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: concept-article
ms.assetid: 1fe1e9f1-daed-4df8-bf32-df7258d9a3fe
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About the Unique Identifier Value for a Resource
In Configuration Manager, the Configuration Manager unique identifier property for a new resource class is optional. If you report inventory data for the resource, you must include this property. The Configuration Manager unique identifier value must be unique — it relates your resource discovery data to your inventory data (SMS_G_xxx). Typically, hardware resources use a GUID to uniquely identify individual resources.  

 The format of the Configuration Manager unique identifier value is as follows.  

```  
<ID Type>:<ID Value>  
```  

 For example, Configuration Manager uses a GUID to identify Configuration Manager clients.  

```  
GUID:4976DCD4-CAAE-11D2-8E00-00104BCC3648  
```  

 You can use any \<ID Type> and \<ID Value> values to identify a new resource. However, when discovering data for an existing resource type, you should follow the convention that is used by that resource type.  

## See Also  
 [How to Get the Unique Identifier Value for a Client](../../../../develop/core/servers/configure/how-to-get-the-unique-identifier-value-for-a-client.md)   
