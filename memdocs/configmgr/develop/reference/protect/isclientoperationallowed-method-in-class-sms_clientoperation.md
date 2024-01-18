---
title: IsClientOperationAllowed Method
titleSuffix: Configuration Manager
description: checks whether a user has permission to execute an operation.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: ec0c0fe9-f5ab-4ab4-8ce1-5bb3592c60c4
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IsClientOperationAllowed Method in Class SMS_ClientOperation
The `IsClientOperationAllowed` Windows Management Instrumentation (WMI) class method in Configuration Manager that checks whether a user has permission to execute an operation.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 IsClientOperationAllowed   
{  
    [IN]    UInt32 Type  
    [IN]    String TargetCollectionID  
    [IN]    UInt32 TargetResourceIDs[]  
};  
```  

## Parameters  
 `Type`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 Type.    

 `TargetCollectionID`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 TargetCollectionID.    

 `TargetResourceIDs`  
 Data type: `UInt32 Array`  

 Qualifiers: [id("2"), in, optional]  

 TargetResourceIDs.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
