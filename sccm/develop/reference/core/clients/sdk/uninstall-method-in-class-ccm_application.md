---
title: "Uninstall Method"
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
ms.assetid: 24654af4-e004-417f-8874-d0e77279822bsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Uninstall Method in Class CCM_Application
The `Uninstall` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that uninstalls an application.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 Uninstall   
{  
    [IN]    String Id  
    [IN]    String Revision  
    [IN]    Boolean IsMachineTarget  
    [IN]    UInt32 EnforcePreference  
    [IN]    String Priority  
    [IN]    Boolean IsRebootIfNeeded  
    [OUT]   String JobId  
};  
```  

## Parameters  
 `Id`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Application identifier.    

 `Revision`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Revision.    

 `IsMachineTarget`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), in]  

 `true` if the application targets a machine.    

 `EnforcePreference`  
 Data type: `UInt32`  

 Qualifiers: [id("3"), in, values]  

 Enforce preference. Possible values are:   

|||  
|-|-|  
|0|Immediate|  
|1|NonBusinessHours|  
|2|AdminSchedule|  

 `Priority`  
 Data type: `String`  

 Qualifiers: [id("4"), in, valuemap]  

 Priority. Possible values are:   

||  
|-|  
|Foreground|  
|High|  
|Normal|  
|Low|  

 `IsRebootIfNeeded`  
 Data type: `Boolean`  

 Qualifiers: [id("5"), in]  

 `true` if a reboot is needed.    

 `JobId`  
 Data type: `String`  

 Qualifiers: [id("6"), out]  

 Job identifier.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
