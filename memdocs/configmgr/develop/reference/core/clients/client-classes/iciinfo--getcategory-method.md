---
title: "ICIINFO::GetCategory"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 76c96b11-787a-4a37-b592-f0bdd4e094ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ICIINFO::GetCategory Method
The `ICIINFO::GetCategory` method, in Configuration Manager, gets a localized category name by index and the group name of the category.  

## Syntax  

```  
[IDL]  
HRESULT GetCategory(  
     ULONG ulIndex,  
     LanguageId* pLanguageId,  
     LPWSTR* ppszCategoryGroup,  
     LPWSTR* ppszCategoryName  
);  
```  

#### Parameters  
 `ulIndex`  
 Data type: `ULONG`  

 Qualifiers: [in]  

 Index of the category to retrieve.  

 `pLanguageId`  
 Data type: `LanguageId`  

 Qualifiers: [in, out]  

 Pointer to a language ID used to obtain the localized category name. If there is no localized name for this ID, the method attempts to obtain the language-independent string. If this does not exist, the method returns an error. On successful return from the method, this parameter indicates the language ID for the localized category name.  

 `ppszCategoryGroup`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to the category group.  

 `ppszCategoryName`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to the localized name of the category.  

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
