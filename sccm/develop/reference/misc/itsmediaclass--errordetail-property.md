---
title: "ITsMediaClass::ErrorDetail Property"
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
ms.assetid: 2d4d616c-d210-48be-a486-6bb7d7fd88f1searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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
