---
title: SMS_MigrationJobEntityRelation Class
titleSuffix: Configuration Manager
description: In Configuration Manager, The SMS_MigrationJobEntityRelation WMI class is an SMS Provider server class that represents the relationship between each migration job and the objects that it contains.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 3ab60b66-864e-4851-8c8b-68a35f6302d8
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_MigrationJobEntityRelation Server WMI Class
The `SMS_MigrationJobEntityRelation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the relationship of between each migration job and the objects that it contains.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationJobEntityRelation : SMS_BaseClass  
{  
    UInt32 EntityID;  
    String EntityName;  
    SInt32 EntityRichStatus;  
    SInt32 EntityStatus;  
    SInt32 JobEntityStatus;  
    UInt32 JobID;  
    SInt32 MessageCode;  
    String MessageDetail1;  
    String MessageDetail2;  
    String MessageDetail3;  
    SInt32 Type;  
    String UniqueID;  
};  
```  

## Methods  
 The `SMS_MigrationJobEntityRelation` class does not define any methods.  

## Properties  
 `EntityID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Migration entity ID.  

 `EntityName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The name of the entity.  

 `EntityRichStatus`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Enums for rich entity status.  

|Value|Enums status|  
|-|-|  
|0|Available to migrate|  
|1|Migrated|  
|2|Running|  
|3|Failed|  
|4|Excluded|  
|5|PendingContent|  
|6|Modified|  
|7|Removed|  
|8|PendingSchedule|  
|9|Scheduled|  

 `EntityStatus`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Enums for entity status, not job related.  

|Value|Enums status|  
|-|-|  
|0|Not started|  
|1|completed|  
|2|running|  
|3|failed|  
|4|excluded|  
|5|skipped (never happened)|  

 `JobEntityStatus`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Enums for job entity status.  

|Value|Enums status|  
|-|-|  
|0|Not started|  
|1|completed|  
|2|running|  
|3|failed|  
|4|excluded (never happens)|  
|5|skipped|  

 `JobID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Migration job ID.  

 `MessageCode`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Code for first message for this object in this job.  

 `MessageDetail1`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Additional detail 1 for message.  

 `MessageDetail2`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Additional detail 2 for message.  

 `MessageDetail3`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Additional detail 3 for message.  

 `Type`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The object type.  

 `UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The unique ID of the object.  

## Remarks  
 For each instance, this class carries the detailed information for the containing object, such as the name, status, detailed error message, or error code.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
