---
title: "GetEvaluationState Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: abe568e3-3859-44a1-a97b-e9127055480b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# GetEvaluationState Method in Class CCM_ApplicationPolicy

The `GetEvaluationState` Windows Management Instrumentation (WMI) class method in Configuration Manager.

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
