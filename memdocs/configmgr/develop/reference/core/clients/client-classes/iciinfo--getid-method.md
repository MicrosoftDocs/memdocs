---
title: "ICIINFO::GetId"
titleSuffix: Configuration Manager
description: "In Configuration Manager, the ICIINFO::GetId method gets the ID of the configuration item."
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 03754f1a-0146-4ff3-8d18-bee4fed9a932
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
