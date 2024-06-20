---
title: RequestLocks Method
titleSuffix: Configuration Manager
description: The RequestLocks Windows Management Instrumentation (WMI) class method, in Configuration Manager, synchronously acquires locks to edit multiple global objects.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c7e2f093-bd48-4d8f-a06e-c3d731626145
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RequestLocks Method in Class SMS_ObjectLock
The `RequestLocks` Windows Management Instrumentation (WMI) class method, in Configuration Manager, synchronously acquires locks to edit multiple global objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RequestLocks(  
    string ObjectRelPaths[],   
    boolean RequestTransfer,   
    SMS_ObjectLockRequest ObjectLockRequests[]   
);  
```  

#### Parameters  
 `ObjectRelPaths`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The paths of the objects for which the locks are requested.  

 `RequestTransfer`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 If the lock is not owned by the local site, the lock request should be forwarded to the parent/child site.  

 `ObjectLockRequests`  
 Data type: `SMS_ObjectLockRequest` Array  

 Qualifiers: [out]  

 A WMI class that represents object lock request information.  

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
