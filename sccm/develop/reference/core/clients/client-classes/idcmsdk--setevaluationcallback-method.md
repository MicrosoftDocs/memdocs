---
title: "IDCMSDK::SetEvaluationCallback"
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
ms.assetid: f7d77efb-c9ed-4d3b-80c9-ba792c72d6a8searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IDCMSDK::SetEvaluationCallback Method
The `IDCMSDK::SetEvaluationCallback` method, in Configuration Manager, associates a callback object with an existing evaluation job, specified by job ID.  

## Syntax  

```  
[IDL]  
HRESULT SetEvaluationCallback(  
     JobIdRef  jobId,  
     IDCMAgentCallback*  pCallback  
);  
```  

#### Parameters  
 `jobId`  
 Data type: `JobIdRef`  

 Qualifiers: [in]  

 ID of the evaluation job to retrieve.  

 `pCallback`  
 Data type: `IDCMAgentCallback`  

 Qualifiers: [in]  

 Pointer to an [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md) object. This parameter can be set to `null` if no callback is available.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Remarks  
 The typical way to use this method is to pass `null` for the `pCallback` parameter.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md)   
 [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md)
