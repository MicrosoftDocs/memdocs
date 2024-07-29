---
title: ResolvePendingRegistrationRecord Method
titleSuffix: Configuration Manager
description: The ResolvePendingRegistrationRecord Windows Management Instrumentation (WMI) class method resolves any conflicts for the pending registration records.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: ec646177-2beb-4b90-a6ff-00384dd40859
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ResolvePendingRegistrationRecord Method in Class SMS_PendingRegistrationRecord
The `ResolvePendingRegistrationRecord` Windows Management Instrumentation (WMI) class method, in Configuration Manager, resolves any conflicts for the pending registration records.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 ResolvePendingRegistrationRecord(     
     string SMSID,  
     uint32 Action  
);  
```  

#### Parameters  
 `SMSID`  
 Data type: `String`  

 Qualifiers: [in]  

 Pending registration record id to use.  

 `Action`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Action to execute on the pending registration record. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|1|Merge: Allows the record to take over the existing conflicting record.|  
|2|New: Creates a new record for the `SMSID` resource. This resource is then issued a new `SMSID` value.|  
|3|Reject: Creates a new record for the `SMSID` resource. This resource is then issued a new `SMSID` value, but is restricted from communicating with the Configuration Manager site.|  

## Return Values  
 An `SInt32`data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
