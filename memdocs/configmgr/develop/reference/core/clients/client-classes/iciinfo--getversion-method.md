---
description: "Learn how to use the ICIIINFO::GetVersion method to get the version of the configuration item in Configuration Manager."
title: "ICIINFO::GetVersion"
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 98d0c5c4-9f8e-41e6-b536-55d9e3f9541d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICIINFO::GetVersion Method
The `ICIINFO::GetVersion` method, in Configuration Manager, gets the version of the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetVersion(  
     LPWSTR* ppszVersion  
);  
```  

#### Parameters  
 `ppszVersion`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to the version of the configuration item.  

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
