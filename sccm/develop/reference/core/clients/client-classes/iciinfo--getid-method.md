---
title: "ICIINFO::GetId"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 03754f1a-0146-4ff3-8d18-bee4fed9a932
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ICIINFO::GetId Method
The `ICIINFO::GetId` method, in Configuration Manager, gets the ID of the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetId(  
    LPWSTR* ppszId  
);  
```  

#### Parameters  
 `ppszId`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to the ID of the configuration item.  

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
