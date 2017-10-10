---
title: "SMS_ObjectLock Class"
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
ms.assetid: 65797a0a-cf39-4081-8963-c084c81531edsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ObjectLock Server WMI Class
The `SMS_ObjectLock` abstract Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents methods for locking and unlocking global objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ObjectLock : SMS_BaseClass  
{  
};  
```  

## Methods  
 The following table shows the methods in `SMS_ObjectLock`.  

|Method|Description|  
|------------|-----------------|  
|[CancelLockRequest Method in Class SMS_ObjectLock](../../../develop/reference/misc/cancellockrequest-method-in-class-sms_objectlock.md)|Cancels a lock request.|  
|[CancelLockRequests Method in Class SMS_ObjectLock](../../../develop/reference/misc/cancellockrequests-method-in-class-sms_objectlock.md)|Cancels multiple lock requests.|  
|[CheckLockRequest Method in Class SMS_ObjectLock](../../../develop/reference/misc/checklockrequest-method-in-class-sms_objectlock.md)|Checks a lock request.|  
|[CheckLockRequests Method in Class SMS_ObjectLock](../../../develop/reference/misc/checklockrequests-method-in-class-sms_objectlock.md)|Checks multiple lock requests.|  
|[GetLockInformation Method in Class SMS_ObjectLock](../../../develop/reference/misc/getlockinformation-method-in-class-sms_objectlock.md)|Gets current lock information.|  
|[ReleaseAllLocks Method in Class SMS_ObjectLock](../../../develop/reference/misc/releasealllocks-method-in-class-sms_objectlock.md)|Releases all locks for a session.|  
|[ReleaseLock Method in Class SMS_ObjectLock](../../../develop/reference/misc/releaselock-method-in-class-sms_objectlock.md)|Releases a lock to global object.|  
|[ReleaseLocks Method in Class SMS_ObjectLock](../../../develop/reference/misc/releaselocks-method-in-class-sms_objectlock.md)|Releases locks to multiple global objects.|  
|[RequestLock Method in Class SMS_ObjectLock](../../../develop/reference/misc/requestlock-method-in-class-sms_objectlock.md)|Synchronously acquires a lock to edit global object.|  
|[RequestLockAsync Method in Class SMS_ObjectLock](../../../develop/reference/misc/requestlockasync-method-in-class-sms_objectlock.md)|Asynchronously acquires a lock to edit global objects.|  
|[RequestLocks Method in Class SMS_ObjectLock](../../../develop/reference/misc/requestlocks-method-in-class-sms_objectlock.md)|Synchronously acquires a lock to edit a global object.|  
|[RequestLocksAsync Method in Class SMS_ObjectLock](../../../develop/reference/misc/requestlocksasync-method-in-class-sms_objectlock.md)|Asynchronously acquires locks to edit multiple global objects.|  

## Properties  
 None.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
