---
title: SetBusinessHours Method
description: Learn how the SetBusinessHours Windows Management Instrumentation (WMI) class method, in Configuration Manager, that sets the values for business hours.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c93b11dc-e63e-4620-8ae1-83f4bea0969a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SetBusinessHours Method in Class CCM_ClientUXSettings
The `SetBusinessHours` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that sets the values for business hours.    

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 SetBusinessHours   
{  
    [IN]    UInt32 WorkingDays  
    [IN]    UInt32 StartTime  
    [IN]    UInt32 EndTime  
};  
```  

## Parameters  
 `WorkingDays`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 Working days.    

 `StartTime`  
 Data type: `UInt32`  

 Qualifiers: [id("1"), in]  

 Start time.    

 `EndTime`  
 Data type: `UInt32`  

 Qualifiers: [id("2"), in]  

 End time.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
