---
title: "ICIINFO::GetLastEvalTime"
titleSuffix: Configuration Manager
description: "In Configuration Manager, the ICIINFO::GetLastEvalTime method gets the last evaluation time for the configuration item."
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: ab774cae-788d-4504-ad35-c34972275afc
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICIINFO::GetLastEvalTime Method
The `ICIINFO::GetLastEvalTime` method, in Configuration Manager, gets the last evaluation time for the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetLastEvalTime(  
     SYSTEMTIME* pstEvalTime  
);  
```  

#### Parameters  
 `pstEvalTime`  
 Data type: `SYSTEMTIME`  

 Qualifiers: [out]  

 Pointer to a `SYSTEMTIME` object indicating the last evaluation time.  

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
