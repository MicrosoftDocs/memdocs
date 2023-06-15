---
title: "ICIINFO::GetProperty"
description: Learn how the ICIINFO::GetProperty method, in Configuration Manager, gets a named property value from the configuration item.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a8812aaa-31e5-46f6-bdae-cea5c24da9ed
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICIINFO::GetProperty Method
The `ICIINFO::GetProperty` method, in Configuration Manager, gets a named property value from the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetProperty(  
     LanguageId* pLanguageId,  
     LPCWSTR pszPropName,  
     LPWSTR* ppszPropValue  
);  
```  

#### Parameters  
 `pLanguageId`  
 Data type: `LanguageId`  

 Qualifiers: [in, out]  

 Pointer to the language ID that is used to obtain the property. If there is no localized name for this ID, the method attempts to obtain the language-independent version of the property. If this does not exist, the method returns an error. On successful return from the method, this parameter indicates the language ID for the property retrieved.  

 `pszPropName`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 Pointer to a null-terminated string specifying the name of the property.  

 `ppszPropValue`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to a null-terminated string specifying the property value.  

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
