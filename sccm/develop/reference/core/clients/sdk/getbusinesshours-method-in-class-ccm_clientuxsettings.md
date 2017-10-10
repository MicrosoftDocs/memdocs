---
title: "GetBusinessHours Method"
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
ms.assetid: d77b13b0-d410-4353-826c-58474e35c0a2searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetBusinessHours Method in Class CCM_ClientUXSettings
The `GetBusinessHours` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that that gets the values for business hours.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetBusinessHours   
{  
    [OUT]   UInt32 WorkingDays  
    [OUT]   UInt32 StartTime  
    [OUT]   UInt32 EndTime  
};  
```  

## Parameters  
 `WorkingDays`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), out]  

 Working days.    

 `StartTime`  
 Data type: `UInt32`  

 Qualifiers: [id("1"), out]  

 Start time.    

 `EndTime`  
 Data type: `UInt32`  

 Qualifiers: [id("2"), out]  

 End time.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
