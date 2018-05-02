---
title: "SMS_LastCategoryObject Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7d777ba2-006e-4b23-9f14-cfdd05ba16d5
author: aczechowski
ms.author: aaroncz
manager: dougeby
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

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
