---
title: "SMS_MigrationEntity Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: f1d73341-0463-4939-942f-c26ed9c50324searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MigrationEntity Server WMI Class
The `SMS_MigrationEntity` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the gathered object entities from the Configuration Manager 2007 hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationEntity : SMS_BaseClass  
{  
    Boolean ChangedAffinity;  
    UInt32 DashboardState;  
    UInt32 EntityID;  
    String EntityKey;  
    String EntityName;  
    String ExcludedBy;  
    Boolean IsActive;  
    UInt32 JobIDs[];  
    UInt32 ObjectTypeID;  
    UInt32 ReferencedEntities[];  
    UInt32 ReferencingEntities[];  
    UInt32 SourceSiteID;  
    UInt32 Status;  
    UInt32 Type;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_MigrationEntity` class.  

|Method|Description|  
|------------|-----------------|  
|[ExcludeAndInclude Method in Class SMS_MigrationEntity](../../../../develop/reference/core/migration/excludeandinclude-method-in-class-sms_migrationentity.md)|Marks the entities as excluded or included.|  
|[GetEntityReferences Method in Class SMS_MigrationEntity](../../../../develop/reference/core/migration/getentityreferences-method-in-class-sms_migrationentity.md)|Gets the referenced entities of the specified entities.|  

## Properties  
 `ChangedAffinity`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if this object should be included in changed object type job.  

 `DashboardState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration]  

 Entity dashboard state. Possible values are:  

|||  
|-|-|  
|0|Remaining|  
|1|Migrated|  
|2|Excluded|  

 `EntityID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Entity ID.  

 `EntityKey`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Entity key imported from a Configuration Manager 2007 site.  

 `EntityName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Name of the entity.  

 `ExcludedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Excluded by user.  

 `IsActive`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if this object is from an active site.  

 `JobIDs`  
 Data type: `UInt32 Array`  

 Access type: Read-only  

 Qualifiers: [lazy]  

 Jobs containing this entity.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Sub-type of entity.  

 `ReferencedEntities`  
 Data type: `UInt32 Array`  

 Access type: Read-only  

 Qualifiers: [lazy]  

 Entities directly referenced by this entity.  

 `ReferencingEntities`  
 Data type: `UInt32 Array`  

 Access type: Read-only  

 Qualifiers: [lazy]  

 Entities directly referencing this entity.  

 `SourceSiteID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Source site ID.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration]  

 Entity migration status. Possible values are:  

|||  
|-|-|  
|0|AVAILABLETOMIGRATE|  
|1|MIGRATED|  
|2|RUNNING|  
|3|FAILED|  
|4|EXCLUDED|  
|6|MODIFIED|  
|7|REMOVED|  
|8|PENDINGSCHEDULE|  
|9|SCHEDULED|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Type of entity.  

## Remarks  
 Each instance represents an object like a collection, a package, or a configuration item, carrying the basic metadata for the entities, such as name, status, and the unique key.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
