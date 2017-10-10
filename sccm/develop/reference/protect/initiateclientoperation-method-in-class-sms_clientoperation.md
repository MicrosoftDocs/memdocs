---
title: "InitiateClientOperation Method"
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
ms.assetid: 0ec680b1-981e-4da4-81f0-7eab784ef2dcsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# InitiateClientOperation Method in Class SMS_ClientOperation
The `InitiateClientOperation` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that initiates a client operation.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 InitiateClientOperation   
{  
    [IN]    UInt32 Type  
    [IN]    String TargetCollectionID  
    [IN]    UInt32 RandomizationWindow  
    [IN]    UInt32 TargetResourceIDs[]  
    [OUT]   UInt32 OperationID  
};  
```  

## Parameters  
 `Type`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 Type.    

 `TargetCollectionID`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 TargetCollectionID.    

 `RandomizationWindow`  
 Data type: `UInt32`  

 Qualifiers: [id("2"), in, optional]  

 RandomizationWindow.    

 `TargetResourceIDs`  
 Data type: `UInt32 Array`  

 Qualifiers: [id("3"), in, optional]  

 TargetResourceIDs.    

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
