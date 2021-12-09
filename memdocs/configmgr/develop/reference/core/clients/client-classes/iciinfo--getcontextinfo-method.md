---
title: "ICIINFO::GetContextInfo"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 46bfc017-20b2-44e3-8256-d40ba3f46de6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ICIINFO::GetContextInfo Method
The `ICIINFO::GetContextInfo` method, in Configuration Manager, gets the context information by name from the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetContextInfo(  
     LPCWSTR pszName,  
     LPWSTR* ppszContext  
);  
```  

#### Parameters  
 `pszName`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 Pointer to a null-terminated string specifying the name of the context information to retrieve.  

 `ppszContext`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to a null-terminated string specifying the retrieved context information.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Remarks  
 This method is used in setting information that is retrieved by certain class handlers in the System Definition Model (SDM) agent.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
