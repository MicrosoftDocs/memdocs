---
title: "ICIINFO::GetSdmTypeName"
titleSuffix: Configuration Manager
description: "In Configuration Manager, the ICIINFO::GetSdmTypeName method gets the fully qualified name of a configuration item."
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 274296fd-0eb5-4b6b-b349-9839c70555af
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICIINFO::GetSdmTypeName Method
The `ICIINFO::GetSdmTypeName` method, in Configuration Manager, gets the fully qualified name of a configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetSdmTypeName(  
     LPWSTR* ppszTypeName  
);  
```  

#### Parameters  
 `ppszTypeName`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to a string which represents the fully qualified name of the configuration item.  

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
