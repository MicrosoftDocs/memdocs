---
title: "DetermineIfRebootPending Method"
titleSuffix: "Configuration Manager"
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
ms.assetid: 3a3d65ac-be3c-471c-9819-2bbb28be3b15searchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# DetermineIfRebootPending Method in Class CCM_ClientUtilities
The `DetermineIfRebootPending` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that …   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 DetermineIfRebootPending   
{  
    [OUT]   Boolean RebootPending  
    [OUT]   Boolean IsHardRebootPending  
    [OUT]   Boolean InGracePeriod  
    [OUT]   DateTime DisableHideTime  
    [OUT]   DateTime RebootDeadline  
};  
```  

## Parameters  
 `RebootPending`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), out]  

 RebootPending.    

 `IsHardRebootPending`  
 Data type: `Boolean`  

 Qualifiers: [id("1"), out]  

 IsHardRebootPending.    

 `InGracePeriod`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), out]  

 InGracePeriod.    

 `DisableHideTime`  
 Data type: `DateTime`  

 Qualifiers: [id("3"), out]  

 DisableHideTime.    

 `RebootDeadline`  
 Data type: `DateTime`  

 Qualifiers: [id("4"), out]  

 RebootDeadline.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
