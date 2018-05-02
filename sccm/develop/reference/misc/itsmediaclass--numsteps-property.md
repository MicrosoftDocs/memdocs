---
title: "ITsMediaClass::NumSteps Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 81dd40df-0e9f-49ef-a31f-70cfc4547baf
author: aczechowski
ms.author: aaroncz
manager: dougeby
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
