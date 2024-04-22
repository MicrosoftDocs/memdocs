---
title: SMS_LastCategoryObject Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents the object that has this assignment as the last category assignment.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 7d777ba2-006e-4b23-9f14-cfdd05ba16d5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_LastCategoryObject Server WMI Class
The `SMS_LastCategoryObject` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the object that has this assignment as the last category assignment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_LastCategoryObject : SMS_BaseClass  
{  
    String CategoryID;  
    String ObjectKey;  
    UInt32 ObjectTypeID;  
};  
```  

## Methods  
 The `SMS_LastCategoryObject` class does not define any methods.  

## Properties  
 `CategoryID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the RBA security category.  

 `ObjectKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Object key.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the object type.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
