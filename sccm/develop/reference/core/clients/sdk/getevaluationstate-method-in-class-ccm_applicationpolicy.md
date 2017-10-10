---
title: "GetEvaluationState Method"
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
ms.assetid: abe568e3-3859-44a1-a97b-e9127055480bsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetEvaluationState Method in Class CCM_ApplicationPolicy
The `GetEvaluationState` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that …   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetEvaluationState   
{  
    [IN]    String PolicyId  
    [IN]    String PolicyRevision  
    [IN]    Boolean IsMachineTarget  
    [OUT]   Object PolicyEvalState  
    [OUT]   Object AppEvalState  
};  
```  

## Parameters  
 `PolicyId`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Policy identifier.    

 `PolicyRevision`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Policy revision.    

 `IsMachineTarget`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), in]  

 `true` if this is a device targeted application.    

 `PolicyEvalState`  
 Data type: `CCM_EvaluationState`  

 Qualifiers: [id("3"), out]  

 Policy evaluation state.   

 `AppEvalState`  
 Data type: `CCM_EvalutationState`  

 Qualifiers: [id("4"), out]  

 Application evaluation state.   

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
