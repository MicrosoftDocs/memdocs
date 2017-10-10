---
title: "GetUserCapability Method"
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
ms.assetid: be25c931-3cc9-407d-b10e-b57b22a5b1c5searchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetUserCapability Method in Class CCM_ClientUtilities
The `GetUserCapability` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that …   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetUserCapability   
{  
    [IN]    UInt32 Feature  
    [OUT]   UInt32 Value  
};  
```  

## Parameters  
 `Feature`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 Feature.    

 `Value`  
 Data type: `UInt32`  

 Qualifiers: [id("1"), out]  

 Value.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
