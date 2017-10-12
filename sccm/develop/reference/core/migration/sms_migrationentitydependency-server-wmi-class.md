---
title: "SMS_MigrationEntityDependency Class"
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
ms.assetid: b46865d2-7f86-43d5-8615-4ee16624ba48searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MigrationEntityDependency Server WMI Class
The `SMS_MigrationEntityDependency` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the dependency relationship between objects in the Configuration Manager 2007 hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationEntityDependency : SMS_BaseClass  
{  
    UInt32 Dependant;  
    UInt32 DependencyType;  
    UInt32 EntityID;  
};  
```  

## Methods  
 The `SMS_MigrationEntityDependency` class does not define any methods.  

## Properties  
 `Dependant`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Dependent entity identifier.  

 `DependencyType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Entity dependency type.  

 `EntityID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Entity ID.  

## Remarks  
 The dependency tree is flattened for performance, which means, if A depends on B, and B depends on C, by querying this class, you can get an instance representing A depends on C. By referring to this class, you can guarantee the data integrity when creating a migration job.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
