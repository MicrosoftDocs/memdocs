---
description: Learn how to add the type of relationship between a user and a device in Configuration Manager using AddType.
title: AddType Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8b292712-09c5-438e-adc1-0458c96a50dd
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AddType Method in Class SMS_UserMachineRelationship
The `AddType` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds a type of the relationship between a user and a device.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
sint32 AddType(  
     uint32 TypeId  
);  
```  

#### Parameters

 `TypeId`  
 Data type: `UInt32` Array  

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
