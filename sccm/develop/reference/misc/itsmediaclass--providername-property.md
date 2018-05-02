---
title: "ITsMediaClass::ProviderName Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1e7abfe3-485a-4bf3-ac9a-5d374c460941
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ITsMediaClass::ProviderName Property
In Configuration Manager, the `ProviderName` property contains the name of the SMS Provider to which to connect.  

## Syntax  

```  
[IDL]  
HRESULT ProviderName([in] BSTR ProviderName);  

HRESULT ProviderName([out,retval] BSTR* ProviderName);  
```  

#### Parameters  
 `ProviderName`  
 Data type: `BSTR`  

 Qualifiers: [in; out, retval]  

 On input, the provider name to set. On output, this parameter points to the retrieved provider name.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)
