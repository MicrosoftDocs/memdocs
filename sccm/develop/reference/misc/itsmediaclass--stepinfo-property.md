---
title: "ITsMediaClass::StepInfo Property"
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
ms.assetid: 679e8772-2c66-46cf-88cf-cdae35b631c5searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ITsMediaClass::StepInfo Property
In Configuration Manager, the `StepInfo` property contains a description of the current media creation step.  

## Syntax  

```  
[IDL]  
HRESULT StepInfo([out,retval] BSTR* Info);  
```  

#### Parameters  
 `Info`  
 Data type: `BSTR`  

 Qualifiers: [out, retval]  

 Pointer to the step information.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 `StepInfo` is used only with asynchronous media creation.  

 The description is non-localized.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)
