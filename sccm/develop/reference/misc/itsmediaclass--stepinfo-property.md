---
title: "ITsMediaClass::StepInfo Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 679e8772-2c66-46cf-88cf-cdae35b631c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
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
