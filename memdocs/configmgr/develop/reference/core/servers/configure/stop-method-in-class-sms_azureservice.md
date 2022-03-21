---
title: Stop method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6dbd4a5d-a1aa-403e-9431-b97276d2b200
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---

# Stop method in class SMS_AzureService

The `Stop` WMI class method in Configuration Manager, that's invoked to stop a Microsoft Azure service which represents a cloud distribution point for Configuration Manager.  

The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 Stop   
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
