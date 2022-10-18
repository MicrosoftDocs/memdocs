---
title: VerifySignature Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the VerifySignature WMI class method verifies the data signature.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a9e9ab89-6b46-4e90-ac0f-c038bd5c9fec
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# VerifySignature Method in Class CCM_SoftwareCatalogUtilities
The `VerifySignature` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that verifies the data signature.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 VerifySignature   
{  
    [IN]    String Data  
    [IN]    String DataSignature  
    [IN]    String WebServiceID  
    [IN]    Boolean VerifyUserAndTimestamp  
    [OUT]   Boolean SignatureVerificationPassed  
};  
```  

## Parameters  
 `Data`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Data to verify.   

 `DataSignature`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Data signature.    

 `WebServiceID`  
 Data type: `String`  

 Qualifiers: [id("2"), in]  

 Web Service identifier.    

 `VerifyUserAndTimestamp`  
 Data type: `Boolean`  

 Qualifiers: [id("3"), in]  

 `true` to verify the user and timestamp.   

 `SignatureVerificationPassed`  
 Data type: `Boolean`  

 Qualifiers: [id("4"), out]  

 `true` if the data signature is valid.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
