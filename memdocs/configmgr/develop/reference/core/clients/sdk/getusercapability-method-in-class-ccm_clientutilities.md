---
title: GetUserCapability Method
titleSuffix: Configuration Manager
description: The GetUserCapability WMI class method in Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: be25c931-3cc9-407d-b10e-b57b22a5b1c5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# GetUserCapability Method in Class CCM_ClientUtilities

The `GetUserCapability` Windows Management Instrumentation (WMI) class method in Configuration Manager.

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
