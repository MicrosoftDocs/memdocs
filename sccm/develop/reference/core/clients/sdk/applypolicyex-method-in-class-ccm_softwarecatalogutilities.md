---
title: "ApplyPolicyEx Method"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: ca1d579b-7986-41c5-9227-2430996f0ad5searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ApplyPolicyEx Method in Class CCM_SoftwareCatalogUtilities
The `ApplyPolicyEx` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that applies policy.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 ApplyPolicyEx   
{  
    [IN]    String Body  
    [IN]    String BodySignature  
    [IN]    String BodySource  
    [OUT]   String Id  
};  
```  

## Parameters  
 `Body`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Policy body.    

 `BodySignature`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Policy body signature.    

 `BodySource`  
 Data type: `String`  

 Qualifiers: [id("2"), in]  

 Policy body source.    

 `Id`  
 Data type: `String`  

 Qualifiers: [id("3"), out]  

 Identifier.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
