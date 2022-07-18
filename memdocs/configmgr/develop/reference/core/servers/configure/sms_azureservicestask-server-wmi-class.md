---
title: SMS_AzureServicesTask Class
titleSuffix: Configuration Manager
description: "An SMS Provider server class that represents a Microsoft Azure specific operation that can be performed on the specified Microsoft Azure service. This class can be used to initiate an operation as well as monitor the results of the operation."
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d9f0070c-a6ff-45d7-b5e7-62deafabb297
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---

# SMS_AzureServicesTask server WMI class

The `SMS_AzureServicesTask` WMI class is an SMS Provider server class in Configuration Manager, that represents a Microsoft Azure specific operation which can be performed on the specified Microsoft Azure service. This can be used to initiate an operation as well as monitor the results of the operation.  

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AzureServicesTask : SMS_BaseClass  
{  
    UInt32 AzureServiceId;  
    String SiteCode;  
    DateTime TaskCreationTime;  
    DateTime TaskEndTime;  
    UInt32 TaskID;  
    String TaskKeyValue;  
    UInt32 TaskStateId;  
    UInt32 TaskTypeId;  
    UInt32 Type;  
};  
```  

## Methods  
 The `SMS_AzureServicesTask` class does not define any methods.  

## Properties  
 `AzureServiceId`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The service identifier key for the `SMS_AzureService` instance on which the current task will be performed.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Site code of the site that owns the task.  

 `TaskCreationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time the task was created.  

 `TaskEndTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time the task ended.  

 `TaskID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, not_null]  

 Identifier of the Microsoft Azure service task.  

 `TaskKeyValue`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Input for the task - if required. This value is not needed for `CreateDeployment`, `UpgradeDeployment`, `DeleteDeployment`, `StopDeployment`, or `StartDeployment` and any value will be ignored.  

 `TaskStateId`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Identifier of the current task state. Possible values are:  

|Value|Task state|  
|-|-|  
|1|Created|  
|2|In Progress|  
|3|Completed|  
|4|Failed|  

 `TaskTypeId`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null, values]  

 Identifier for type of task. Possible values are:  

|Value|Task type|  
|-|-|  
|1|CreateDeployment|  
|2|UpgradeDeployment|  
|3|DeleteDeployment|  
|4|StopDeployment|  
|5|StartDeployment|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Type of task. Possible values are:  

|Value|Task type|  
|-|-|  
|0|RunOnce|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
