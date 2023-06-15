---
description: "Learn how to use the ICIINFO::GetCategoryCount method to get the count of categories that are associated with the configuration item."
title: "ICIINFO::GetCategoryCount"
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: cd89fdf9-84ca-44d2-8dbe-2e95bcfc53e6
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICIINFO::GetCategoryCount Method
The `ICIINFO::GetCategoryCount` method, in Configuration Manager, gets the count of categories that are associated with the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetCategoryCount(  
     ULONG* pulCount  
);  
```  

#### Parameters  
 `pulCount`  
 Data type: `ULONG`  

 Qualifiers: [out]  

 Pointer to the count of categories applied to the configuration item.  

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
