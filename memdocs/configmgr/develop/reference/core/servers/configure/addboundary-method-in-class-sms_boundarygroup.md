---
description: Learn how to add boundaries to a boundary group in Configuration Manager using AddBoundary class method.
title: AddBoundary method in class SMS_BoundaryGroup
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8bb764e3-c2c4-4b06-b9ec-4bc060b1fbeb
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AddBoundary Method in Class SMS_BoundaryGroup
The `AddBoundary` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds boundaries to this boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddBoundary(  
   UInt32 BoundaryID[]  
);  
```  

#### Parameters  
 `BoundaryID`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 Unique identifier of the boundary.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BoundaryGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_boundarygroup-server-wmi-class.md)
