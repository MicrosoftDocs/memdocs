---
title: "ITsMediaClass::StepProgress Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ed5fe79c-f44c-4672-86ed-60aa22a55624
author: aczechowski
ms.author: aaroncz
manager: dougeby
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
