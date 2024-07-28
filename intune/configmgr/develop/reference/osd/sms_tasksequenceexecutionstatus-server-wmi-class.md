---
title: SMS_TaskSequenceExecutionStatus Class
titleSuffix: Configuration Manager
description: In Configuration Manager, The SMS_TaskSequenceExecutionStatus WMI class is an SMS Provider server class that represents the status of an execution of a task sequence.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 7963e19d-8f82-4d7d-b850-af376a85e41b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequenceExecutionStatus Server WMI Class
The `SMS_TaskSequenceExecutionStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the status of an execution of a task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequenceExecutionStatus : SMS_BaseClass  
{  
    String ActionName;  
    String ActionOutput;  
    String AdvertisementID;  
    DateTime ExecutionTime;  
    UInt32 ExitCode;  
    String GroupName;  
    UInt32 LastStatusMsgID;  
    String LastStatusMsgName;  
    String PackageID;  
    UInt32 ResourceID;  
    UInt32 Step;  
};  
```  

## Methods  
 The `SMS_TaskSequenceExecutionStatus` class does not define any methods.  

## Properties  
 `ActionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the action in the task sequence that was executed.  

 `ActionOutput`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Console output of the task sequence step that was executed.  

 `AdvertisementID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Deployment identifier of the task sequence.  

 `ExecutionTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Run time of the task sequence.  

 `ExitCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Exit code of the task sequence step that was executed.  

 `GroupName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Group name in the task sequence that was executed.  

 `LastStatusMsgID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier for this execution status.  

 `LastStatusMsgName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name for this execution status.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Task sequence package identifier.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Client computer identifier.  

 `Step`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Step number in the task sequence that was executed.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
