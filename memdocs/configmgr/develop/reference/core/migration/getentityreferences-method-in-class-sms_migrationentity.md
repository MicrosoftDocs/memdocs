---
description: Learn how to get the referenced entities of the specified entities in Configuration Manager using GetEntityReferences class method.
title: GetEntityReferences Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 84d3851e-e98b-4c1f-a9cb-2df7821ca6ce
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetEntityReferences Method in Class SMS_MigrationEntity
The `GetEntityReferences` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the referenced entities of the specified entities.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetEntityReferences(  
     UInt32 entityIDs[],  
     UInt32 referenceType,  
     Boolean referenceDirection,  
     UInt32 entityReferenceList[]  
);  
```  

#### Parameters  
 `entityIDs`  
 Data type: `UInt32` array  

 Qualifiers: [in]  

 List of entities input.  

 `referenceType`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Reference type.  

 `referenceDirection`  
 Data type: `Boolean` array  

 Qualifiers: [in]  

 A flag indicating whether this is querying referencing or being referenced.  

 `entityReferenceList`  
 Data type: `UInt32` Array  

 Qualifiers: `[out]`  

 List of entities queried.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_MigrationEntity Server WMI Class](../../../../develop/reference/core/migration/sms_migrationentity-server-wmi-class.md)
