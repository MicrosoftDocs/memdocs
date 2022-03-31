---
title: "CancelLockRequest Method"
titleSuffix: "Configuration Manager"
description: "The CancelLockRequest Windows Management Instrumentation (WMI) class method cancels a lock request."  
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c64dc0cb-82a6-40e2-8a27-ae1490105b94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CancelLockRequest Method in Class SMS_ObjectLock
The `CancelLockRequest` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cancels a lock request.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CancelLockRequest(  
    string RequestID   
);  
```  

#### Parameters  
 `RequestID`  
 Data type: `String`  

 Qualifiers: [in]  

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
