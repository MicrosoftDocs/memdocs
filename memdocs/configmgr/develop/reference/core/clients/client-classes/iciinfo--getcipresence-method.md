---
title: "ICIINFO::GetCIPresence"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 943e216f-5ac5-4962-a053-072f1acbc6c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


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
 [CIPresence Enumeration](../../../../../develop/reference/core/clients/client-classes/cipresence-enumeration.md)
