---
title: "ITsMediaClass::ErrorDetail Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2d4d616c-d210-48be-a486-6bb7d7fd88f1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ITsMediaClass::ErrorDetail Property
In Configuration Manager, the `ErrorDetail` property contains a buffer in which additional error information can be retrieved from task sequence media creation.  

## Syntax  

```  
[IDL]  
HRESULT ErrorDetail([out,retval] BSTR* Detail);  
```  

#### Parameters  
 `Detail`  
 Data type: `BSTR`  

 Qualifiers: [out, retval]  

 Pointer to the error details.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)
