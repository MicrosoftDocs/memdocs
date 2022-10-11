---
title: RemoveType Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the RemoveType WMI class method removes a type of the relationship between a user and a device.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9601f6bc-c383-40db-b1ec-cac40d6f3e9a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RemoveType Method in Class SMS_UserMachineRelationship
The `RemoveType` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes a type of the relationship between a user and a device.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RemoveType(  
     uint32 TypeId  
);  
```  

#### Parameters  
 `TypeId`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

The type ID.

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
