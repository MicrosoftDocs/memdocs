---
title: "ICIINFO::GetCIPresence"
titleSuffix: Configuration Manager
description: "In Configuration Manager, the ICIINFO::GetCIPresence method gets the current presence for the configuration item, including the compliance state for the configuration item."
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 943e216f-5ac5-4962-a053-072f1acbc6c7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICIINFO::GetCIPresence Method
The `ICIINFO::GetCIPresence` method, in Configuration Manager, gets the current presence for the configuration item. The presence data includes the compliance state for the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetCIPresence(  
     CIPresence* pCIPresence  
);  
```  

#### Parameters  
 `pCIPresence`  
 Data type: `CIPresence`  

 Qualifiers: [out]  

 Pointer to a [CIPresence Enumeration](../../../../../develop/reference/core/clients/client-classes/cipresence-enumeration.md) value indicating the current presence for the configuration item.  

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
 [CIPresence Enumeration](../../../../../develop/reference/core/clients/client-classes/cipresence-enumeration.md)
