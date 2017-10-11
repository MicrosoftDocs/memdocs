---
title: "ITsMediaClass::StepProgress Property"
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
ms.assetid: ed5fe79c-f44c-4672-86ed-60aa22a55624searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ITsMediaClass::StepProgress Property
In Configuration Manager, the `StepProgress` property contains a value indicating the progress of the current step of task sequence media creation.  

## Syntax  

```  
[IDL]  
HRESULT StepProgress([out,retval] long* Progress);  
```  

#### Parameters  
 `Progress`  
 Data type: `long`  

 Qualifiers: [out, retval]  

 Pointer to the step progress value.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 A step is complete when `Progress` reaches 100.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)   
 [ITsMediaClass::CurrentStep Property](../../../develop/reference/misc/itsmediaclass--currentstep-property.md)   
 [ITsMediaClass::NumSteps Property](../../../develop/reference/misc/itsmediaclass--numsteps-property.md)
