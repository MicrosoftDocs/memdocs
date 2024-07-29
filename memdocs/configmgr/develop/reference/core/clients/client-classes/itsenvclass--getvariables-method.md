---
title: "ITSEnvClass::GetVariables"
titleSuffix: Configuration Manager
description: In Configuration Manager, the GetVariables method gets the variables for the operating system deployment task sequence environment.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 858509d5-771f-4bd3-9b5e-59545c11f8e6
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ITSEnvClass::GetVariables Method
In Configuration Manager, the `GetVariables` method gets the variables for the operating system deployment task sequence environment.  

## Syntax  

```  
[IDL]  
HRESULT GetVariables(  
     VARIANT* variables  
);  
```  

#### Parameters  
 `variables`  
 Data type: `VARIANT`  

 Qualifiers: [out, retval]  

 Pointer to the environment variables.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## See Also  
 [ITSEnvClass Interface](../../../../../develop/reference/core/clients/client-classes/itsenvclass-interface.md)
