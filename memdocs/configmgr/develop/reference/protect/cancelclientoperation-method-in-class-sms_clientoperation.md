---
title: CancelClientOperation Method
titleSuffix: Configuration Manager
description: The CancelClientOperation Windows Management Instrumentation (WMI) class method cancels a client operation.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 620de3b8-3755-41f2-92e2-7327eb144104
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CancelClientOperation Method in Class SMS_ClientOperation
The `CancelClientOperation` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that cancels a client operation.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 CancelClientOperation   
{  
    [IN]    UInt32 OperationID  
};  
```  

## Parameters  
 `OperationID`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 OperationID.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
