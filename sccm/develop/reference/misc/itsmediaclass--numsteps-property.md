---
title: "ITsMediaClass::NumSteps Property"
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
ms.assetid: 81dd40df-0e9f-49ef-a31f-70cfc4547bafsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ITsMediaClass::NumSteps Property
In Configuration Manager, the `NumSteps` property contains the number of steps necessary for task sequence media creation.  

## Syntax  

```  
[IDL]  
HRESULT NumSteps([out,retval] long* NumSteps);  
```  

#### Parameters  
 `NumSteps`  
 Data type: `long`  

 Qualifiers: [out, retval]  

 Pointer to the number of steps.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 `NumSteps` can be used only with asynchronous media creation.  

 You can use `NumSteps` with [ITsMediaClass::CurrentStep Property](../../../develop/reference/misc/itsmediaclass--currentstep-property.md) to estimate the overall progress of media creation.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)   
 [ITsMediaClass::CurrentStep Property](../../../develop/reference/misc/itsmediaclass--currentstep-property.md)
