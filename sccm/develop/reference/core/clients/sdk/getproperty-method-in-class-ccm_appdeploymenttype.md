---
title: "GetProperty Method"
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
ms.assetid: 3002c0dd-4713-42c6-bda0-f7cc7d8d1b2dsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetProperty Method in Class CCM_AppDeploymentType
The `GetProperty` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that retrieves an application deployment type property.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetProperty   
{  
    [IN]    UInt32 LanguageId  
    [IN]    String PropertyName  
    [OUT]   String PropertyValue  
};  
```  

## Parameters  
 `LanguageId`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 Language identifier.    

 `PropertyName`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Property name.    

 `PropertyValue`  
 Data type: `String`  

 Qualifiers: [id("2"), out]  

 Property value.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
