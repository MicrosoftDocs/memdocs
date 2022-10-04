---
description: Learn how to use Configuration Manager GetLockInformation Windows Management Instrumentation (WMI) class method to get current lock information.
title: GetLockInformation Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5c414140-1865-4402-9b70-b9b29432c638
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetLockInformation Method in Class SMS_ObjectLock
The `GetLockInformation` Windows Management Instrumentation (WMI) class method, in Configuration Manager,  gets current lock information.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetLockInformation(  
    string ObjectRelPath,   
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
