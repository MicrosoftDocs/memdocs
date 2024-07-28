---
title: RequestLock Method
description: Learn how to use the RequestLock method in Configuration Manager to synchronously acquire a lock to edit a global object.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c13a5af4-d822-41ea-92c3-3bf17b9a5600
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RequestLock Method in Class SMS_ObjectLock
The `RequestLock` Windows Management Instrumentation (WMI) class, in Configuration Manager, synchronously acquires a lock to edit a global object.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RequestLock(  
    string ObjectRelPath,   
    boolean RequestTransfer,   
    string RequestID,   
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

 `RequestState`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Request state values. The request states `Granted`, `GrantedAfterTimeout` and `GrantedLockWasOrphaned` indicate a successful request and the user can then make and save modifications to the object. All other requests indicate an error.  

|RequestStateID|RequestStateName|  
|--------------------|----------------------|  
|0|Unknown|  
|2|Requested|  
|3|RequestedCanceled|  
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

| Value | Lock state |
| ----- | ---------- |
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

 Indicates ObjectLockContext the lock is currently assigned to.  

 `AssignedMachine`  
 Data type: `String`  

 Qualifiers: [out]  

 Indicates the currently assigned computer of the requested lock.  

 `AssignedSiteCode`  
 Data type: `String`  

 Qualifiers: [out]  

 Indicates the current site of the requested lock.  

 `AssignedTimeUTC`  
 Data type: `DateTime`  

 Qualifiers: [out]  

 Indicates the current site of the requested lock.  

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
