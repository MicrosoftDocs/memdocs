---
title: "CancelLockRequests Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2385927c-5439-489f-a3e1-b3d7a6e4a24a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CancelLockRequests Method in Class SMS_ObjectLock
The `CancelLockRequests` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cancels multiple lock requests.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CancelLockRequests(  
    string RequestIDs[]   
);  
```  

#### Parameters  
 `RequestIDs`  
 Data type: `String`  Array  

 Qualifiers: [in]  

 Array of unique identifiers of the request.  

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
