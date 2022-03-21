---
title: "ExcludeAndInclude Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: dc89e1e1-be01-4118-8590-0013ecff5c28
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ExcludeAndInclude Method in Class SMS_MigrationEntity
The `ExcludeAndInclude` Windows Management Instrumentation (WMI) class method, in Configuration Manager, marks the entities as excluded or included.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ExcludeAndInclude(  
     UInt32 excludeEntityList[],  
     UInt32 includeEntityList[]  
);  
```  

#### Parameters  
 `excludeEntityList`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 List of entities excluded.  

 `includeEntityList`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 List of entities included.  

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
