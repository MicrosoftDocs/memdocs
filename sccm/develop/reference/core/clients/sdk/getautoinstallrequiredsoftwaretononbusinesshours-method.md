---
title: "GetAutoInstallRequiredSoftwaretoNonBusinessHours Method"
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
ms.assetid: ce5440c9-2d58-4793-b727-51b6ea030e29searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetAutoInstallRequiredSoftwaretoNonBusinessHours Method in Class CCM_ClientUXSettings
The `GetAutoInstallRequiredSoftwaretoNonBusinessHours` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets the value for `AutomaticallyInstallSoftware`.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetAutoInstallRequiredSoftwaretoNonBusinessHours   
{  
    [OUT]   Boolean AutomaticallyInstallSoftware  
};  
```  

## Parameters  
 `AutomaticallyInstallSoftware`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), out]  

 `true` if required software should be automatically installed during non-business hours.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
