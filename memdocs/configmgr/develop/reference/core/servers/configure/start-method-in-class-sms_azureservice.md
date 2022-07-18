---
title: Start method
titleSuffix: Configuration Manager
description: "In Configuration Manager, The Start WMI class method is invoked to start a Microsoft Azure service which represents a cloud distribution point for Configuration Manager." 
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f32f2b00-117d-498d-9d9b-5f3f47b1b865
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---

# Start method in class SMS_AzureService

The `Start` WMI class method, in Configuration Manager, that's invoked to start a Microsoft Azure service which represents a cloud distribution point for Configuration Manager.  

The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 Start   
{  
    [IN]    UInt32 AzureServiceID  
};  
```  

## Parameters  
 `AzureServiceID`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 The service identifier key for the `SMS_AzureService` instance on which the current task will be performed.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
