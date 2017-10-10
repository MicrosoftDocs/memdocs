---
title: "ExcludeScanPaths Method"
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
ms.assetid: e45972d2-c41a-4532-ad84-b09c9aa17945searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ExcludeScanPaths Method in Class SMS_ClientOperation
The `ExcludeScanPaths` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that excludes scan paths from all members in specified collection.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 ExcludeScanPaths   
{  
    [IN]    UInt64 ThreatID  
    [IN]    String ExclusionSettingsUniqueID  
    [IN]    String ExcludedPaths[]  
    [IN]    String TargetCollectionID  
    [OUT]   UInt32 OperationID  
};  
```  

## Parameters  
 `ThreatID`  
 Data type: `UInt64`  

 Qualifiers: [id("0"), in]  

 ThreatID.    

 `ExclusionSettingsUniqueID`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 ExclusionSettingsUniqueID.    

 `ExcludedPaths`  
 Data type: `String Array`  

 Qualifiers: [id("2"), in]  

 ExcludedPaths.    

 `TargetCollectionID`  
 Data type: `String`  

 Qualifiers: [id("3"), in]  

 TargetCollectionID.    

 `OperationID`  
 Data type: `UInt32`  

 Qualifiers: [id("4"), out]  

 OperationID.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
