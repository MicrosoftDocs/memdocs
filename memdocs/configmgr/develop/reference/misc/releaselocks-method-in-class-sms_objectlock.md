---
title: ReleaseLocks Method
titleSuffix: Configuration Manager
description: A class method that releases locks to multiple global objects.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ce7d1920-8fd3-45c3-93a3-38bc79662791
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ReleaseLocks Method in Class SMS_ObjectLock
The `ReleaseLocks` Windows Management Instrumentation (WMI) class method, in Configuration Manager, releases locks to multiple global objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ReleaseLocks(  
    string ObjectRelPaths[]   
);  
```  

#### Parameters  
 `ObjectRelPaths`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The paths of the objects from which to release the locks.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ObjectLock Server WMI Class](../../../develop/reference/misc/sms_objectlock-server-wmi-class.md)
