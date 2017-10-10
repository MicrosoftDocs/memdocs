---
title: "CheckLockRequests Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: b9c38991-235a-44e2-aaa1-487d9bc5f4e8searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CheckLockRequests Method in Class SMS_ObjectLock
The `CheckLockRequests` Windows Management Instrumentation (WMI) class method, in Configuration Manager, checks multiple lock requests.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CheckLockRequests(  
    string RequestIDs[],   
    uint32 Timeout,   
    SMS_ObjectLockRequest ObjectLockRequests[]   
);  
```  

#### Parameters  
 `RequestIDs`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Array of unique identifiers of the request.  

 `Timeout`  
 Data type: `UInt32`  

 Qualifiers: [in, optional]  

 Seconds to wait for lock request response.  

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
