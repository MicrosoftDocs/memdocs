---
title: QueueRequestedAppPolicy Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the QueueRequestedAppPolicy Windows Management Instrumentation class method that queues an application policy request.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0fd7952e-eeed-4dc0-a66b-af6442156523
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# QueueRequestedAppPolicy Method in Class CCM_RequestedAppPolicy
The `QueueRequestedAppPolicy` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that queues and application policy request.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 QueueRequestedAppPolicy   
{  
    [IN]    String PolicyId  
    [IN]    String PolicyRevision  
    [IN]    String Id  
    [IN]    UInt32 EnforcePreference  
};  
```  

## Parameters  
 `PolicyId`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Policy identifier.    

 `PolicyRevision`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Policy revision.    

 `Id`  
 Data type: `String`  

 Qualifiers: [id("2"), in]  

 Identifier.    

 `EnforcePreference`  
 Data type: `UInt32`  

 Qualifiers: [id("3"), in]  

 Enforce preference. Possible values are:   

|Value|Enforce preference|  
|-|-|  
|0|Immediate|  
|1|Non-Business Hours|  
|2|Admin Schedule|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
