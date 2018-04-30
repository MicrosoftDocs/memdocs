---
title: "ICIINFO::GetEvalState"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7a2f05e8-f5f8-4362-8e67-759624e80371
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ICIINFO::GetEvalState Method
The `ICIINFO::GetEvalState` method, in Configuration Manager, gets the current evaluation state of the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetEvalState(  
     CIEvalState* pCIEvalState  
);  
```  

#### Parameters  
 `pCIEvalState`  
 Data type: `CIEvalState`  

 Qualifiers: [out]  

 Pointer to a [CIEvalState Enumeration](../../../../../develop/reference/core/clients/client-classes/cievalstate-enumeration.md) value indicating the evaluation state.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)   
 [CIEvalState Enumeration](../../../../../develop/reference/core/clients/client-classes/cievalstate-enumeration.md)
