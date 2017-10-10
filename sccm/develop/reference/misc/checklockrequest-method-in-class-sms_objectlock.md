---
title: "CheckLockRequest Method"
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
ms.assetid: 54032c44-cfa7-48cf-92bb-7f8bc482f822searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CheckLockRequest Method in Class SMS_ObjectLock
The `CheckLockRequest` Windows Management Instrumentation (WMI) class method, in Configuration Manager, checks a lock request.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CheckLockRequest(  
    string RequestID,   
    uint32 Timeout,   
    uint32 RequestState,   
    uint32 LockState,   
    string AssignedUser,   
    string AssignedObjectLockContext,   
    string AssignedMachine,   
    string AssignedSiteCode,   
    datetime AssignedTimeUTC  
);  
```  

#### Parameters  
 `RequestID`  
 Data type: `String`  

 Qualifiers: [in, out]  

 Unique identifier of the request.  

 `Timeout`  
 Data type: `UInt32`  

 Qualifiers: [in, optional]  

 Seconds to wait for lock request response.  

 `RequestState`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 The state of the lock request. Possible values are:  

|||  
|-|-|  
|0|Unknown|  
|2|Requested|  
|3|RequestCanceled|  
|4|ResponseReceived|  
|10|Granted|  
|11|GrantedAfterTimeout|  
|12|GrantedLockWasOrphaned|  
|20|DeniedLockAlreadyAssigned|  
|21|DeniedInvalidObjectVersion|  
|22|DeniedLockNotFound|  
|23|DeniedLockNotLocal|  
|24|DeniedRequestTimedOut|  
|50|Error|  
|52|ErrorRequestNotFound|  
|53|ErrorRequestTimedOut|  

 `LockState`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Indicates the current state of the requested lock. Possible values are:  

|||  
|-|-|  
|0|Unassigned|  
|1|Assigned|  
|2|Requested|  
|3|PendingAssignment|  
|4|TimedOut|  
|5|NotFound|  

 `AssignedUser`  
 Data type: `String`  

 Qualifiers: [out]  

 Indicates the currently assigned user of the requested lock.  

 `AssignedObjectLockContext`  
 Data type: `String`  

 Qualifiers: [out]  

 Indicates the unique string identifier of the requested lock.  

 `AssignedMachine`  
 Data type: `String`  

 Qualifiers: [out]  

 Indicates ObjectLockContext the lock is currently assigned to.  

 `AssignedSiteCode`  
 Data type: `String`  

 Qualifiers: [out]  

 Indicates the current site of the requested lock.  

 `AssignedTimeUTC`  
 Data type: `DateTime`  

 Qualifiers: [out]  

 Indicates the time at which the requested lock was assigned.  

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
