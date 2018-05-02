---
title: "SMS_ObjectLockRequest Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 56f7e96e-36a7-48b8-aae8-a7a75fa5c415
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ObjectLockRequest Server WMI Class
The `SMS_ObjectLockRequest` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents object lock request information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ObjectLockRequest :    
{  
    String AssignedMachine;  
    String AssignedObjectLockContext;  
    String AssignedSiteCode;  
    DateTime AssignedTimeUTC;  
    String AssignedUser;  
    UInt32 LockState;  
    String ObjectRelPath;  
    String RequestID;  
    UInt32 RequestState;  
};  
```  

## Methods  
 The `SMS_ObjectLockRequest` class does not define any methods.  

## Properties  
 `AssignedMachine`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the currently assigned computer of the requested lock.  

 `AssignedObjectLockContext`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates ObjectLockContext the lock is currently assigned to.  

 `AssignedSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the current site of the requested lock.  

 `AssignedTimeUTC`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the time at which the requested lock was assigned.  

 `AssignedUser`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the currently assigned user of the requested lock.  

 `LockState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the current state of the requested lock. Possible values are:  

|||  
|-|-|  
|0|Unassigned|  
|1|Assigned|  
|2|Requested|  
|3|PendingAssignment|  
|4|TimedOut|  
|5|NotFound|  

 `ObjectRelPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The path of the object for which the lock is requested.  

 `RequestID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier of the request.  

 `RequestState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

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

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SEDO Server WMI Classes](../../../develop/reference/misc/sedo-server-wmi-classes.md)   
 [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md)
