---
title: "RequestLockAsync Method"
titleSuffix: "Configuration Manager"
Description: Learn how to use the RequestLockAsync method in Configuration Manager to asynchronously acquire a lock to edit global objects.
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c81a383d-ad16-4247-88bb-dcc3de42e16f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# RequestLockAsync Method in Class SMS_ObjectLock
The `RequestLockAsync` Windows Management Instrumentation (WMI) class method, in Configuration Manager, asynchronously acquires a lock to edit global objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RequestLockAsync(  
    string ObjectRelPath,   
    boolean RequestTransfer,   
    string RequestID   
);  
```  

#### Parameters  
 `ObjectRelPath`  
 Data type: `String`  

 Qualifiers: [in]  

 The path of the object for which the lock is requested.  

 `RequestTransfer`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 If the lock is not owned by the local site, the lock request should be forwarded to the parent/child site.  

 `RequestID`  
 Data type: `String`  

 Qualifiers: [out]  

 Unique identifier of the request.  

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
