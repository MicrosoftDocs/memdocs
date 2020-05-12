---
title: "RemoveBoundary Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c10773f5-d34b-4c0d-928c-f214319540f6
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# RemoveBoundary Method in Class SMS_BoundaryGroup
The `RemoveBoundary` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes boundaries from this boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RemoveBoundary(  
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
