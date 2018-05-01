---
title: "SMS_CH_EvalResult Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 92dead34-4152-4c81-9a41-678087880c07
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CH_EvalResult Server WMI Class
The `SMS_CH_EvalResult` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents client evaluation results.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CH_EvalResult : SMS_BaseClass  
{  
    DateTime EvalTime;  
    String HealthCheckDescription;  
    String HealthCheckGUID;  
    UInt32 ResourceID;  
    UInt32 Result;  
    UInt32 ResultCode;  
    String ResultDetail;  
    UInt32 ResultType;  
};  
```  

## Methods  
 The `SMS_CH_EvalResult` class does not define any methods.  

## Properties  
 `EvalTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Evaluation time.   

 `HealthCheckDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Health Check description.   

 `HealthCheckGUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Health check GUID.   

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Unique Configuration Manager-supplied ID for the resource.  

 `Result`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Evaluation result.   

 `ResultCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Result code.   

 `ResultDetail`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Result detail.   

 `ResultType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Result type.   

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Client Status Server WMI Classes](../../../../../develop/reference/core/clients/status/client-status-server-wmi-classes.md)
