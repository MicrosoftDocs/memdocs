---
title: "EvaluateAllPolicies Method"
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
ms.assetid: 1d2b4471-ed93-42d5-b1d7-bf3990b69f84searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# EvaluateAllPolicies Method in Class CCM_ApplicationPolicy
The `EvaluateAllPolicies` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that evaluated all policies.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 EvaluateAllPolicies   
{  
    [IN]    Boolean IsEnforceAction  
    [OUT]   String JobIdUser  
    [OUT]   String JobIdMachine  
};  
```  

## Parameters  
 `IsEnforceAction`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), in]  

 `True` if the action will be enforced.    

 `JobIdUser`  
 Data type: `String`  

 Qualifiers: [id("1"), out]  

 Job identifier of a user policy.    

 `JobIdMachine`  
 Data type: `String`  

 Qualifiers: [id("2"), out]  

 Job identifier of a machine policy.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
