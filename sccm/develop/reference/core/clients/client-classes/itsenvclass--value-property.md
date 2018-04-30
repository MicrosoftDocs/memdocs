---
title: "ITSEnvClass::Value Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: af3dd230-5c84-485b-8335-9417ba863215
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ITSEnvClass::Value Property
In Configuration Manager, the `Value` property contains the value of an operating system deployment task sequence environment variable.  

## Syntax  

```  
[IDL]  
HRESULT Value([in] BSTR Name, [in] BSTR Value);  

HRESULT Value([in] BSTR Name, [out,retval] BSTR* Value);  
```  

#### Parameters  
 `Name`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 The name of the environment variable.  

 `Value`  
 Data type: `BSTR`  

 Qualifiers: [in; out, retval]  

 On input, the value to set for the environment variable. On output, this parameter points to the value that is retrieved for the supplied name.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 The `get_Value` function succeeds with S_OK when called with an invalid variable name, but retrieves an empty string for the value. Note that this behavior differs from the more common return of a non-zero exit code to indicate an invalid variable name input.  

## See Also  
 [ITSEnvClass Interface](../../../../../develop/reference/core/clients/client-classes/itsenvclass-interface.md)
